<template>
  <div>
    <i class="el-icon-circle-plus-outline"  @click="dialogFormVisible = true"></i>
    <el-dialog
      title="添加/修改管辖居民"
      :visible.sync="dialogFormVisible"
      @close="clear">
      <el-form v-model="form" style="text-align: left;" ref="dataForm">
        <el-form-item prop="id" style="height: 0">
          <el-input type="hidden" v-model="form.id" autocomplete="off"></el-input>
        </el-form-item>
        <el-form-item label="姓名" :label-width="formLabelWidth" prop="name">
          <el-input v-model="form.name" autocomplete="off" ></el-input>
        </el-form-item>
        <el-form-item label="曾姓名" :label-width="formLabelWidth" prop="uname">
          <el-input v-model="form.uname" autocomplete="off" ></el-input>
        </el-form-item>
        <el-form-item label="身份证" :label-width="formLabelWidth" prop="idnum">
          <el-input v-model="form.idnum" autocomplete="off"></el-input>
        </el-form-item>
        <el-form-item label="性别" :label-width="formLabelWidth" prop="sex">
          <el-select v-model="form.sex" placeholder="请选择性别">
            <el-option label="男" value="男"></el-option>
            <el-option label="女" value="女"></el-option>
          </el-select>
        </el-form-item>
        <el-form-item label="民族" :label-width="formLabelWidth" prop="natived">
          <el-input v-model="form.natived" autocomplete="off"></el-input>
        </el-form-item>
        <el-form-item label="出生日期" :label-width="formLabelWidth" prop="date">
          <div class="block">
            <el-date-picker
              v-model="form.birthdate"
              type="date"
              placeholder="选择出生日期">
            </el-date-picker>
          </div>
        </el-form-item>
        <el-form-item label="身高" :label-width="formLabelWidth" prop="height">
          <el-input v-model="form.height" autocomplete="off"></el-input>
        </el-form-item>
        <el-form-item label="证件照" :label-width="formLabelWidth" prop="photo">
          <el-input v-model="form.photo" autocomplete="off"></el-input>
        </el-form-item>
        <el-form-item label="籍贯" :label-width="formLabelWidth" prop="naplace">
          <el-input v-model="form.naplace" autocomplete="off" ></el-input>
        </el-form-item>
        <el-form-item label="宗教信仰" :label-width="formLabelWidth" prop="religion">
          <el-input v-model="form.religion" autocomplete="off" ></el-input>
        </el-form-item>
        <el-form-item label="出生地" :label-width="formLabelWidth" prop="birplace">
          <el-input v-model="form.birplace" autocomplete="off" ></el-input>
        </el-form-item>
        <el-form-item label="家庭住址" :label-width="formLabelWidth" prop="address1" >
          <el-input v-model="form.address1" autocomplete="off"></el-input>
        </el-form-item>
        <el-form-item label="文化程度" :label-width="formLabelWidth" prop="edudegree">
          <el-select v-model="form.edudegree" placeholder="请选择文化程度">
            <el-option label="小学" value="小学"></el-option>
            <el-option label="初中" value="初中"></el-option>
            <el-option label="高中" value="高中"></el-option>
            <el-option label="中专" value="中专"></el-option>
            <el-option label="本科" value="本科"></el-option>
            <el-option label="硕士" value="硕士"></el-option>
            <el-option label="博士" value="博士"></el-option>
          </el-select>
        </el-form-item>
        <el-form-item label="服务处所" :label-width="formLabelWidth" prop="emplace" >
          <el-input v-model="form.emplace" autocomplete="off"></el-input>
        </el-form-item>
        <el-form-item label="何时迁入本市（县）" :label-width="formLabelWidth" prop="whenincity">
          <div class="block">
            <el-date-picker
              v-model="form.whenincity"
              type="date"
              placeholder="何时迁入本市（县）">
            </el-date-picker>
          </div>
        </el-form-item>
        <el-form-item label="何地迁入本市（县）" :label-width="formLabelWidth" prop="whereincity" >
          <el-input v-model="form.whereincity" autocomplete="off"></el-input>
        </el-form-item>
        <el-form-item label="何时迁入本址" :label-width="formLabelWidth" prop="whenin">
          <div class="block">
            <el-date-picker
              v-model="form.whenin"
              type="date"
              placeholder="何时迁入本址">
            </el-date-picker>
          </div>
        </el-form-item>
        <el-form-item label="何地迁入本址" :label-width="formLabelWidth" prop="wherein" >
          <el-input v-model="form.wherein" autocomplete="off"></el-input>
        </el-form-item>
        <el-form-item label="职业" :label-width="formLabelWidth" prop="occupation" >
          <el-input v-model="form.occupation" autocomplete="off"></el-input>
        </el-form-item>
        <el-form-item label="兵役情况" :label-width="formLabelWidth" prop="arstatus">
          <el-select v-model="form.arstatus" placeholder="请选择婚姻情况">
            <el-option label="条件不符" value="条件不符"></el-option>
            <el-option label="未服兵役" value="未服兵役"></el-option>
            <el-option label="已服兵役" value="已服兵役"></el-option>
            <el-option label="服役中" value="服役中"></el-option>
          </el-select>
        </el-form-item>
        <el-form-item label="婚姻情况" :label-width="formLabelWidth" prop="marstatus">
          <el-select v-model="form.marstatus" placeholder="请选择婚姻情况">
            <el-option label="离婚" value="离婚"></el-option>
            <el-option label="未婚" value="未婚"></el-option>
            <el-option label="丧偶" value="丧偶"></el-option>
          </el-select>
        </el-form-item>

        <el-form-item label="户主与户主关系" :label-width="formLabelWidth" prop="reholder">
          <el-select v-model="form.reholder" placeholder="户主与户主关系">
            <el-option label="夫妻" value="夫妻"></el-option>
            <el-option label="父子" value="父子"></el-option>
            <el-option label="母子" value="母子"></el-option>
          </el-select>
        </el-form-item>
      </el-form>
      <div slot="footer" class="dialog-footer">
        <el-button @click="dialogFormVisible = false">取 消</el-button>
        <el-button type="primary" @click="onSubmit">确 定</el-button>
      </div>
    </el-dialog>
  </div>
</template>

<script>
  export default {
    name: 'EditForm',
    data () {
      return {
        dialogFormVisible: false,
        form: {
          id: '',
          name: '',
          uname: '',
          naplace: '',
          birplace: '',
          address1: '',
          edudegree: '',
          emplace: '',
          whenincity: '',
          whereincity: '',
          whenin: '',
          wherein: '',
          occupation: '',
          arstatus: '',
          marstatus: '',
          height: '',
          religion: '',
          birthdate: '',
          natived: '',
          sex: '',
          reholder: '',
          photo: '',
          idnum: ''
        },
        formLabelWidth: '120px'
      }
    },
    methods: {
      clear () {
        this.form = {
          id: '',
          name: '',
          uname: '',
          naplace: '',
          birplace: '',
          address1: '',
          edudegree: '',
          emplace: '',
          whenincity: '',
          whereincity: '',
          whenin: '',
          wherein: '',
          occupation: '',
          arstatus: '',
          marstatus: '',
          height: '',
          religion: '',
          birthdate: '',
          natived: '',
          sex: '',
          reholder: '',
          photo: '',
          idnum: ''
        }
      },
      onSubmit () {
        this.$axios
          .post('/residents', {
            id: this.form.id,
            name: this.form.name,
            uname: this.form.uname,
            naplace: this.form.naplace,
            birplace: this.form.birplace,
            address1: this.form.address1,
            edudegree: this.form.edudegree,
            emplace: this.form.emplace,
            whenincity: this.form.whenincity,
            whereincity: this.form.whereincity,
            whenin: this.form.whenin,
            wherein: this.form.wherein,
            occupation: this.form.occupation,
            arstatus: this.form.arstatus,
            marstatus: this.form.marstatus,
            height: this.form.height,
            religion: this.form.religion,
            birthdate: this.form.birthdate,
            natived: this.form.natived,
            sex: this.form.sex,
            reholder: this.form.reholder,
            photo: this.form.photo,
            idnum: this.form.idnum
          }).then(resp => {
          if (resp && resp.status === 200) {
            this.dialogFormVisible = false
            this.$emit('onSubmit')
          }
        })
      }
    }
  }
</script>

<style scoped>
  .el-icon-circle-plus-outline {
    margin: 50px 0 0 20px;
    font-size: 90px;
    float: left;
    cursor: pointer;
  }
</style>


