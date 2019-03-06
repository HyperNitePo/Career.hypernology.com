<template>
    <v-content class="pa-0">
        <BackGround img="https://career.hypernology.com/img/3dev.jpg" subtitle="加入我們" title="Apply for Us"></BackGround>
        <v-container>
        <v-card>
            <v-stepper v-model="step">
                <v-stepper-header>
                    <v-stepper-step :complete="step > 1" step="1">部門類別</v-stepper-step>

                    <v-divider></v-divider>

                    <v-stepper-step :complete="step > 2" step="2">職位類別</v-stepper-step>

                    <v-divider></v-divider>

                    <v-stepper-step :complete="step > 3" step="3">個人資料</v-stepper-step>

                    <v-divider></v-divider>

                    <v-stepper-step :complete="step > 4" step="4">聯絡資料</v-stepper-step>

                    <v-divider></v-divider>

                    <v-stepper-step :complete="step === 5" step="5">完成</v-stepper-step>
                </v-stepper-header>
                <v-stepper-items>
                    <v-stepper-content step="1">
                        <v-card class="grey lighten-3">
                            <v-card-title class="headline">請選擇你欲加入的部門</v-card-title>
                            <span class="pl-4 error--text" v-if="form.departsel.length === 0">(請最少勾選一個)</span>
                            <v-card-text class="pl-4">
                                <template v-for="(det,ind) in departs">
                                    <v-checkbox :hint="det.desp" :key="ind" :label="det.chname"
                                                :messages="'('+det.desp+')'" :value="det.id" slot="activator"
                                                v-model="form.departsel"></v-checkbox>
                                </template>
                            </v-card-text>
                            <v-card-actions>
                                <v-btn disabled v-if="form.departsel.length === 0">[!] 請選擇最少一個部門。</v-btn>
                                <v-btn @click="step--" class="warning" v-else-if="step > 1">上一頁</v-btn>
                                <v-btn @click="step++" class="primary" v-else-if="step < 4">下一頁</v-btn>
                            </v-card-actions>
                        </v-card>
                    </v-stepper-content>
                    <v-stepper-content step="2">
                        <v-card class="grey lighten-3">
                            <v-card-title class="headline">請輸入職位類別及可到任日期</v-card-title>
                            <v-card-text class="pl-4">
                                <v-form>
                                    <v-layout :class="$vuetify.breakpoint.mdAndDown ? 'column' : 'row'">
                                        <v-flex class="pr-3" xs4>
                                            <h2 class="font-weight-light">工作時間</h2><span class="error--text"
                                                                                         v-if="form.time.length === 0">(必填)</span>
                                            <v-radio-group :rules="[form.time.length!==0 || '不能為空']"
                                                           v-model="form.time">
                                                <v-radio label="全職 Full-time (有機會升為主管級) (必須填寫中文名稱)"
                                                         value="fulltime"></v-radio>
                                                <v-radio label="兼職 Part-time (工作量較少)" value="parttime"></v-radio>
                                            </v-radio-group>
                                        </v-flex>
                                        <v-flex class="pr-5" xs4>
                                            <h2 class="font-weight-light">可到任日期</h2>
                                            <v-dialog
                                                    :return-value.sync="form.date"
                                                    full-width
                                                    lazy
                                                    persistent
                                                    ref="dialog"
                                                    v-model="modal"
                                                    width="290px"
                                            >
                                                <v-text-field
                                                        label="點擊以選擇日期"
                                                        prepend-icon="event"
                                                        readonly
                                                        slot="activator"
                                                        v-model="form.date"
                                                ></v-text-field>
                                                <v-date-picker :max="max" :min="min" no-title scrollable
                                                               v-model="form.date">
                                                    <v-spacer></v-spacer>
                                                    <v-btn @click="modal = false" color="primary" flat>取消</v-btn>
                                                    <v-btn @click="$refs.dialog.save(form.date)" color="primary" flat>
                                                        儲存
                                                    </v-btn>
                                                </v-date-picker>
                                            </v-dialog>
                                        </v-flex>
                                        <v-flex xs4>
                                            <h2 class="font-weight-light">你希望成為哪一類型的職員？</h2><span class="error--text"
                                                                                                  v-if="form.type.length === 0">(必填)</span>
                                            <v-radio-group :rules="rules" v-model="form.type">
                                                <v-radio label="普通職員 (不需要填寫中文姓名，但沒有晉升的機會)" value="informal"></v-radio>
                                                <v-radio label="正式職員 (需要填寫中文姓名，並有晉升機會)" value="formal"></v-radio>
                                            </v-radio-group>
                                        </v-flex>
                                    </v-layout>
                                </v-form>
                            </v-card-text>
                            <v-card-actions>
                                <v-btn @click="step--" class="warning" v-if="step > 1">上一頁</v-btn>
                                <v-btn disabled v-if="form.type.length === 0 || form.time.length === 0">你尚未填寫完成</v-btn>
                                <v-btn @click="step++" class="primary" v-else-if="step < 4">下一頁</v-btn>
                            </v-card-actions>
                        </v-card>
                    </v-stepper-content>
                    <v-stepper-content step="3">
                        <v-card class="grey lighten-3">
                            <v-card-title class="headline">個人資料</v-card-title>
                            <v-card-text class="pl-4">
                                <v-form v-model="valid">
                                    <v-layout :class="($vuetify.breakpoint.mdAndDown ? 'column' : 'row')+' wrap'">
                                        <v-flex class="pr-3" xs3>
                                            <v-text-field
                                                    :label="(form.type.match('informal') ? '你希望我們如何稱呼你？' : '姓名 中文 : ( 真實姓名 )')"
                                                    :rules="rules" counter="7" required
                                                    v-model="form.chname"></v-text-field>
                                        </v-flex>
                                        <v-flex class="pr-3" xs3>
                                            <v-text-field :rules="rules" label="Name In English" required
                                                          v-model="form.engname"></v-text-field>
                                        </v-flex>
                                        <v-flex class="pr-3" xs3>
                                            <v-text-field
                                                    :rules="[v => v.length !== 0 || '此欄為必填', v => v > 10 || '年齡過小', v=> v < 65 || '年齡過大']"
                                                    label="年齡 Age" required type="number"
                                                    v-model="form.age"></v-text-field>
                                        </v-flex>
                                        <v-flex xs3>
                                            <v-text-field :rules="[v => v.length > 10 || '請填寫正確的電話號碼']"
                                                          append-icon="phone" label="電話號碼" mask="(+###)###############"
                                                          required v-model="form.phone"></v-text-field>
                                        </v-flex>
                                        <v-flex xs3>
                                            <h2 class="font-weight-light title">性別</h2><span class="error--text"
                                                                                             v-if="form.sex.length === 0">(必填)</span>
                                            <v-radio-group :rules="rules" v-model="form.sex">
                                                <v-radio label="男" value="boy"></v-radio>
                                                <v-radio label="女" value="girl"></v-radio>
                                            </v-radio-group>
                                            <v-text-field
                                                    :rules="[v => v.length !== 0 || '此欄為必填', v => v.toString().includes('@') || '電子郵件格式不正確']"
                                                    label="電子郵件" required v-model="form.email"></v-text-field>
                                        </v-flex>
                                    </v-layout>
                                </v-form>
                            </v-card-text>
                            <v-card-actions>
                                <v-btn @click="step--" class="warning" v-if="step > 1">上一頁</v-btn>
                                <v-btn disabled
                                       v-if="!valid || form.sex.length === 0 || form.phone.length < 10 || !form.email.includes('@')">
                                    你尚未填寫完成
                                </v-btn>
                                <v-btn @click="step++" class="primary" v-else-if="step < 4">下一頁</v-btn>
                            </v-card-actions>
                        </v-card>
                    </v-stepper-content>
                    <v-stepper-content step="4">
                        <v-card class="grey lighten-3">
                            <v-card-title class="headline">聯絡資料</v-card-title>
                            <v-card-text>
                                <v-form v-model="valid2">
                                    <v-layout :class="$vuetify.breakpoint.mdAndDown ? 'column' : 'row'">
                                        <v-flex class="pr-3" xs6>
                                            <h2 class="font-weight-light">請選擇你欲使用的聯絡方式</h2><span class="error--text"
                                                                                                 v-if="form.contact.length === 0">(必填)</span>
                                            <v-radio-group :rules="rules" v-model="form.contact">
                                                <v-radio label="Discord" value="Discord"></v-radio>
                                                <v-radio label="Facebook Messager" value="Facebook Messager"></v-radio>
                                                <v-radio label="WhatsApp" value="WhatsApp"></v-radio>
                                            </v-radio-group>
                                        </v-flex>
                                        <v-flex xs6>
                                            <v-text-field :label="'請輸入你的 '+form.contact+' 的ID / 用戶名稱 / 連結'"
                                                          :rules="rules" box required v-if="form.contact.length !== 0"
                                                          v-model="form.contact_id"></v-text-field>
                                        </v-flex>
                                    </v-layout>
                                    <v-checkbox :rules="[v => !!v || '你必須同意此選項']"
                                                label="你交出表單即代表你已遵從條款 : 如個人資料更改時，本人認知更新個人檔案資料之責任。"
                                                required></v-checkbox>
                                </v-form>
                            </v-card-text>
                            <v-card-actions>
                                <v-btn @click="step--" class="warning" v-if="step > 1">上一頁</v-btn>
                                <v-btn disabled v-if="!valid2 || form.contact.length === 0">你尚未填寫完成</v-btn>
                                <v-btn :disabled="submitting" :loading="submitting" @click="submit" class="success"
                                       v-else>遞交
                                </v-btn>
                            </v-card-actions>
                        </v-card>
                    </v-stepper-content>
                    <v-stepper-content step="5">
                        <v-card class="grey lighten-3">
                            <v-card-title class="headline">你的表單已遞交</v-card-title>
                            <v-card-text>若選擇了 Discord 作為你的聯絡方式，請到 https://discordapp.com/invite/mezMwzg 與職員進行聯絡；若你使用了
                                Whatsapp 作為聯絡方式，請安裝 Whatsapp 手機應用程式，將有本組織員工向你進行聯絡。
                            </v-card-text>
                            <v-card-actions>
                                <v-btn class="info" to="/">完成</v-btn>
                            </v-card-actions>
                        </v-card>
                    </v-stepper-content>
                </v-stepper-items>

            </v-stepper>
        </v-card>
    </v-container>
    </v-content>
</template>

<script>
    import global from '../global-func'
    import BackGround from "../components/BackGround";

    export default {
        name: "Apply",
        components: {BackGround},
        data() {
            return {
                valid: false,
                gfunc: global(),
                valid2: false,
                modal: false,
                submitting: false,
                rules: [v => v.length !== 0 || '此欄為必填'],
                form: {
                    time: '',
                    type: '',
                    departsel: [],
                    date: '',
                    chname: '',
                    engname: '',
                    sex: '',
                    age: 15,
                    phone: '',
                    contact: '',
                    contact_id: '',
                    email: ''
                },
                departs: [],
                step: 0,
                error: ''
            }
        },
        computed: {
            max: () => {
                let now = new Date();
                now.setMonth(now.getMonth() + 2);
                return now.toISOString().substr(0, 7)
            },
            min: () => {
                let now = new Date();
                now.setFullYear(now.getFullYear(), now.getMonth(), now.getDay() - 1);
                return now.toISOString().substr(0, 7)
            },
        },
        created() {
            this.form.date = new Date().toISOString().substr(0, 10)
        },
        methods: {
            submit() {
                this.submitting = true;
                this.$axios({
                    method: 'post',
                    url: 'test.php',
                    data: {
                        time: this.form.time,
                        type: this.form.type,
                        selected_part: this.form.departsel,
                        chinese_name: this.form.chname,
                        english_name: this.form.engname,
                        phone: this.form.phone,
                        age: this.form.age,
                        sex: this.form.sex,
                        contact_method: this.form.contact,
                        contact_id: this.form.contact_id,
                        email: this.form.email
                    }
                }).then(res => {
                    this.submitting = false;
                    this.step = 5;
                    window.alert('中文名: ' + res.data.chinese_name + '\n' + '英文名: ' + res.data.english_name + '\n' + '日期: ' + res.data.date + '\n' + '電話號碼: ' + res.data.phone);
                    this.gfunc.setCookie("hypernite_form_submitted", true, 0)
                }).catch(err => {
                    this.submitting = false;
                    this.error = err;
                    window.alert(err)
                })
            }
        },
        beforeUpdate() {
            if (this.gfunc.getCookie("hypernite_form_submitted")) {
                this.step = 5;
            }
        },
        beforeMount() {
            const departs = import('../../public/json/departments');
            fetch('/json/departments.json').then(r => r.json()).then(data => this.departs = data).catch(() => this.departs = departs);
        }
    }
</script>

<style scoped>

</style>