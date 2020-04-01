<template>
    <div>
      <el-row style="height: 840px">
        <search-bar @onSearch="searchResult" ref="searchBar"></search-bar>
        <el-tooltip effect="dark" placement="right"
                    v-for="item in residents.slice((currentPage-1)*pagesize,currentPage*pagesize)"
                    :key="item.id">
          <p slot="content" style="font-size: 14px;margin-bottom: 6px;">{{item.name}}</p>
          <p slot="content" style="font-size: 13px;margin-bottom: 6px">
            <span>{{item.natived}}</span> /
            <span>{{item.birthdate}}</span> /
            <span>{{item.emplace}}</span>
          </p>
          <p slot="content" style="width: 300px" class="abstract">{{item.address1}}</p>
          <el-card style="width: 135px;margin-bottom: 20px;height: 233px;float: left;margin-right: 15px" class="book"
                   bodyStyle="padding:10px" shadow="hover">
            <div class="cover" @click="editBook(item)">
              <img :src="item.photo" alt="证件照">
            </div>
            <div class="info">
              <div class="title">
                <a href="">{{item.name}}</a>
              </div>
              <i class="el-icon-delete" @click="deleteBook(item.id)"></i>
            </div>
            <div class="author">{{item.sex}}</div>
          </el-card>
        </el-tooltip>
        <edit-form @onSubmit="loadBooks()" ref="edit"></edit-form>
      </el-row>
      <el-row>
        <el-pagination
          @current-change="handleCurrentChange"
          :current-page="currentPage"
          :page-size="pagesize"
          :total="residents.length">
        </el-pagination>
      </el-row>
    </div>
</template>

<script>
  import SearchBar from './SearchBar'
  import EditForm from './EditForm'
  export default {
    name: 'Resident',
    components: {SearchBar, EditForm},
    data () {
      return {
        residents: [],
        currentPage: 1,
        pagesize: 17
      }
    },
    mounted: function () {
      this.loadBooks()
    },
    methods: {
      loadBooks () {
        var _this = this
        this.$axios.get('/residents').then(resp => {
          if (resp && resp.status === 200) {
            _this.residents = resp.data
          }
        })
      },
      handleCurrentChange: function (currentPage) {
        this.currentPage = currentPage
        console.log(this.currentPage)
      },
      searchResult () {
        var _this = this
        this.$axios
          .get('/search?keywords=' + this.$refs.searchBar.keywords, {
          }).then(resp => {
          if (resp && resp.status === 200) {
            _this.residents = resp.data
          }
        })
      },
      deleteBook (id) {
        this.$confirm('此操作将永久删除该书籍, 是否继续?', '提示', {
          confirmButtonText: '确定',
          cancelButtonText: '取消',
          type: 'warning'
        }).then(() => {
            this.$axios
              .post('/delete', {id: id}).then(resp => {
              if (resp && resp.status === 200) {
                this.loadBooks()
              }
            })
          }
        ).catch(() => {
          this.$message({
            type: 'info',
            message: '已取消删除'
          })
        })
        // alert(id)
      },
      editBook (item) {
        this.$refs.edit.dialogFormVisible = true
        this.$refs.edit.form = {
          id: item.id,
          name: item.name,
          uname: item.uname,
          naplace: item.naplace,
          birplace: item.birplace,
          address1: item.address1,
          edudegree: item.edudegree,
          emplace: item.emplace,
          whenincity: item.whenincity,
          whereincity: item.whereincity,
          whenin: item.whenin,
          wherein: item.wherein,
          occupation: item.occupation,
          arstatus: item.arstatus,
          marstatus: item.marstatus,
          height: item.height,
          religion: item.religion,
          birthdate: item.birthdate,
          natived: item.natived,
          sex: item.sex,
          reholder: item.reholder,
          photo: item.photo,
          idnum: item.idnum
        }
      }
    }
  }
</script>

<style scoped>
  .cover {
    width: 115px;
    height: 160px;
    margin-bottom: 7px;
    overflow: hidden;
    cursor: pointer;
  }

  img {
    width: 115px;
    height: 162px;
    margin: 0 auto;
  }

  .title {
    font-size: 14px;
    text-align: left;
  }

  .author {
    color: #333;
    width: 102px;
    font-size: 13px;
    margin-bottom: 6px;
    text-align: left;
  }

  .abstract {
    display: block;
    line-height: 10px;
  }

  a {
    text-decoration: none;
  }

  a:link, a:visited, a:focus {
    color: #3377aa;
  }
</style>
