 <template>
  <div class="HelloWorld"> 
  <font size=5>
			<center>课程表</center>
		</font>
		<table align="center" border="1px" bordercolor="blue" width="600px">
			<tr align="center">
				<td><b>项目</b></td>
				<td colspan="5"><b>上课</b></td>
			</tr>

			<!--表格中字体加粗只需将<td>换成<th>-->
			<tr align="center" >				
				<th>星期</th>
				<th>星期一</th>
				<th>星期二</th>
				<th>星期三</th>
				<th>星期四</th>
				<th>星期五</th>
			</tr>

			<tr v-for="i in arr">
				<td align="center">上午</td>				
				<td>{{i.one}}</td>
				<td>{{i.two}}</td>
				<td>{{i.three}}</td>
				<td>{{i.four}}</td>
				<td>{{i.five}}</td>
			</tr>
			<tr height="3px">
			</tr>

		</table>
		
		<!--修改-->
<el-button type="text" @click="dialogFormVisible = true">点击修改</el-button>

<el-dialog title="表" :visible.sync="dialogFormVisible">
  <el-form :model="form">
    <el-form-item label="星期一" :label-width="formLabelWidth">
      <el-input v-model="form.one" auto-complete="off"></el-input>
    </el-form-item>
    <el-form-item label="星期二" :label-width="formLabelWidth">
      <el-input v-model="form.two" auto-complete="off"></el-input>
    </el-form-item>
    <el-form-item label="星期三" :label-width="formLabelWidth">
      <el-input v-model="form.three" auto-complete="off"></el-input>
    </el-form-item>
    <el-form-item label="星期四" :label-width="formLabelWidth">
      <el-input v-model="form.four" auto-complete="off"></el-input>
    </el-form-item>
    <el-form-item label="星期五" :label-width="formLabelWidth">
      <el-input v-model="form.five" auto-complete="off"></el-input>
    </el-form-item>
  </el-form>
  <div slot="footer" class="dialog-footer">
    <el-button @click="dialogFormVisible = false">取 消</el-button>
    <el-button type="primary" @click="update">确 定</el-button>
  </div>
</el-dialog>
		
		
		
		
  </div>
</template>

<script>
export default {
  name: 'HelloWorld',
  props: {
    msg: String
  },
  created(){
    this.$http.get('http://localhost:3000').then(e=>this.arr=e.body)
  },
  data(){
    return {
    	 dialogTableVisible: false,
        dialogFormVisible: false,
        form: {
          one:'',
          two:'',
          three:'',
          four:'',
          five:'',
        },
       formLabelWidth: '120px',
      arr:[],
      page:false
    }
  },
  created(){
  this.zys()
  },
  methods:{
  	zys(){
  		  this.$http.get('http://localhost:3000').then(e=>this.arr=e.body)
  	},
    update(e){
      this.$http.post('http://localhost:3000/update',this.form,{emulateJSON:true}).then(function(){
        this.zys()
      })
    },
    abc(){
      this.page=!this.page
    }
  }
  
}
</script>


<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
 table{
 	text-align: center;
 	line-height: 30px;
 }
</style>
