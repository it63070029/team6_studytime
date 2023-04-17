<template >

  <div class="container fluid" >
    <section class="hero">
      <div class="hero-body">
        <!-- Searchhh -->
        <div class="columns">
          <div class="column is-3"></div>
          <div class="column is-5">
            <input class="input" type="text"  placeholder="Search" v-model="search"/>
          </div>
          <div class="column is-2">
            <button  class="button" @click="showSeach">Search</button>
          </div>
          <div class="column is-3">
            <button class="button" @click="modalAddSubject=true">เพิ่มรายวิชา</button>
          </div>
        </div>
         <!-- Searchhh -->
      </div>
    </section>
    <section class="section" id="app">
      <div class="content">
        <!-- <div class="columns"> -->
          
          <div class="column is-6 " style="margin-left:25%; " >
            <div v-for="(mySubject,index) in showMySubject" :key="mySubject.id" class="card mb-3 py-2" style="background-color: #3A4F7A;box-shadow: 8px 8px #FFECEF">
              
              <div class="card-content ">
               
                <h4  style="color:#FFF;">
                  <span class="icon">
                    <i class="fa fa-info-circle"></i>
                  </span>
                  <span class="icon" style="float:right" @click="deleteSubject_my(mySubject.id,index)">
                    <i class="fa fa-trash"></i>
                  </span>
                  {{mySubject.id}}
                </h4>
                <h6 style="color:#FFF;">
                  
                  {{mySubject.name}}</h6>
                <div style="color:#FFF"> 
                  <span style="background-color: #FFF;color:#3C4868;padding:3px; border-radius: 60%; padding-left:10px;padding-right:6px;margin-right:15px;font-weight: bold; " >{{mySubject.date}}</span>
                  <span>{{mySubject.time}}</span>
                  
                  <span style="float:right"><div class="button" @click="showDetail(mySubject.id)">ดูเพิ่มเติม > </div></span>
                  <span style="float:right"><div class="button mx-2" @click="linktoNews(mySubject.id,mySubject)">ดูข่าวสาร </div></span>

                </div>
               
              </div>
               
                
              
            </div>
          </div>
        <!-- </div> -->
      </div>
      <!-- Modal Add -Start -->
      <div class="modal" :class="{'is-active': modalAddSubject}">
        <div class="modal-background"></div>
        <div class="modal-card">
          <header class="modal-card-head">
            <p class="modal-card-title">เพิ่มรายวิชา</p>
            <button class="delete" aria-label="close" @click=" modalAddSubject=false"></button>
          </header>
          <section class="modal-card-body">
            <!-- Content ... -->
            <div class="columns">
              <!-- <div>รหัสวิชา :</div> -->
            </div>
            <div class="columns" style="margin-bottom: 20px;">
              <div class="px-2">รหัสวิชา :</div>
              <!-- <input type="text" class="input" v-model="idSubject"> -->
              <div class="select">
                <select v-model="idSubject" class="px-5 mr-3" style="padding-right:100px">
                  <option v-for="subject in subject" :key="subject.id"  style="padding-right:100px">{{subject.id}}</option>
                </select>
                
              </div>
              <!-- <div v-if="idSubject!==''">
              เซค :
               <div class="select">
                <select v-model="idSubject" class="px-5 mr-3" style="padding-right:100px">
                  <option v-for="subject in subject" :key="subject.id"  style="padding-right:100px">{{subject.id}}</option>
                </select>
                
              </div></div> -->

            </div>
             
            <div class="columns" v-for="subject in subject" :key="subject.id">
              
             <div v-if="idSubject== subject.id">
              <div>รหัสวิชา : {{subject.id}}</div>
              
             </div>
             
            </div>
            <div class="columns" v-for="subject in subject" :key="subject.id">
              
             <div v-if="idSubject== subject.id">
              <div>ชื่อวิชา :{{subject.name}}</div>
              
             </div>
             
             
            </div>
            <div class="columns" v-for="subject in subject" :key="subject.id">
              
             <div v-if="idSubject== subject.id">
              <div> เวลา : {{subject.time}}</div>
              
             </div>
             
            </div>
          </section>
          <footer class="modal-card-foot">
            <button class="button is-success" @click="addMySubject">Add</button>
            <button class="button" @click=" modalAddSubject=false">Cancel</button>
          </footer>
        </div>
      </div>
      <!-- Modal Add -End -->

       <!-- Modal Show DetailSubject -Start -->
      <div class="modal" :class="{'is-active': modalShowDetail}" >
        <div class="modal-background"></div>
        <div class="modal-card" v-for="selectSubject in selectSubject" :key="selectSubject.id">
          <header class="modal-card-head">
            <p class="modal-card-title">{{selectSubject.name}}</p>
            <button class="delete" aria-label="close" @click=" modalShowDetail=false"></button>
          </header>
          <section class="modal-card-body">
            <!-- Content ... -->
           
            <div class="columns" style="margin-bottom: 20px;margin-left:5%">
              <div class="content">รายละเอียดรายวิชา</div>
            </div>
            <div class="columns" style="margin-bottom: 20px;margin-left:5%">
              <div>รหัสวิชา : {{selectSubject.id}}</div>
            </div>
             <div class="columns" style="margin-bottom: 20px;margin-left:5%">
              <div>อาจารย์ผู้สอน : {{selectSubject.teach}}</div>
            </div>
             <div class="columns" style="margin-bottom: 20px;margin-left:5%">
              <div>ช่องทางติดต่อ : <span>{{selectSubject.email}}</span></div>
            </div>
            
             <div class="columns" style="margin-bottom: 20px;margin-left:5%"> 
              <p>วัน-เวลาที่เรียน : </p>
              <div>{{"  "+selectSubject.date + "  " +selectSubject.time}}</div>
            
            </div>
             <div class="columns" style="margin-bottom: 20px; margin-left:5%">
              <div>สถานที่เรียน : {{selectSubject.room}}</div>
            </div>
            <div class="columns" style="margin-bottom: 20px;margin-left:20%">
              <figure class="image">
                  <img
                    style="height: 150px;width: 150px;border-radius: 25px;"
                    :src=selectSubject.image[0].no1
                    alt="Placeholder image"
                  />
                </figure>
                <figure class="image mx-2" >
                  <img 
                    style="height: 150px;width: 150px;border-radius: 25px;"
                    :src=selectSubject.image[0].no2
                    alt="Placeholder image"
                  />
                </figure>
            </div>
            <div class="columns" style="margin-bottom: 20px; margin-left:5%;margin-top:20px">
              <div>เส้นทางการเดินทาง : <a>{{selectSubject.route}}</a></div>
            </div>
            <!-- <div class="columns" style="margin-bottom: 20px; margin-left:5%">
              <a>{{selectSubject.route}}</a>
            </div> -->
             
            
          </section>
          
        </div>
      </div>
      <!-- Modal Show DetailSubject -End -->


      <!-- Modal Show Delete -Start -->
      <div class="modal" :class="{'is-active': modalDelete}" >
        <div class="modal-background"></div>
        <div class="modal-card" v-for="selectSubject in selectSubject" :key="selectSubject.id">
          <header class="modal-card-head">
            <p class="modal-card-title">Delete </p>
            <button class="delete" aria-label="close" @click=" modalDelete=false"></button>
          </header>
          <section class="modal-card-body">
            <!-- Content ... -->
          
            <div class="columns pt-3" style="margin-bottom: 20px;margin-left:5%">
              
              <p>คุณต้องการลบวิชา {{selectSubject.name+'('+selectSubject.id+')'}} ออกจากตารางเรียน  </p>
            </div>
            <div class="columns pt-4" style="margin-bottom: 20px;margin-left:5%">
              <button class="button is-success mx-3" @click="confirmDelete">Delete</button>
              <button class="button" @click=" modalDelete=false">Cancel</button>
              
            </div>
          </section>
          
        </div>
      </div>
      <!-- Modal Show Delete -End -->
    </section>
      
  </div>

 
</template>

<script>
import axios from "axios";
// @ is an alias to /src
export default {
  name: "Home",
  // props: ['user'],
  data() {
    return {
      
       subject: [
        {id:"06016325",name:"SERVICE-ORIENTED PROGRAMMING",credit:"3",teach:"ผศ.ดร. ธราวิเชษฐ์ ธิติจรูญโรจน์",room:"ตึก IT คณะเทคโนโลยีสารสนเทศ ห้อง Audi",time:"9.00-12.00",date:"ศ.",image:[{no1:"https://www.techtalkthai.com/wp-content/uploads/2016/11/kmitl_it_data_science_01.jpg",no2:"https://www.it.kmitl.ac.th/wp-content/themes/itkmitl2017wp/img/life/life-10.jpg"}],route:"https://g.page/ITKMITL?share",email:"taravichet@it.kmitl.ac.th"},
        {id:"90304004",name:"REPORT WRITING",credit:"3",teach:"ผศ. จันจิรา จันทร์เจริญสุข",room:"ตึก IT คณะเทคโนโลยีสารสนเทศ ห้อง Audi",time:"9.00-12.00",date:"พ.",image:[{no1:"https://www.techtalkthai.com/wp-content/uploads/2016/11/kmitl_it_data_science_01.jpg",no2:"https://www.it.kmitl.ac.th/wp-content/themes/itkmitl2017wp/img/life/life-10.jpg"}],route:"https://g.page/ITKMITL?share",email:"pjjuyt@gmail.com"},
        {id:"06016310",name:"HUMAN INTERFACE DESIGN",credit:"3",teach:"รศ.ดร.นพพร โชติกกำธร",room:"ตึก IT คณะเทคโนโลยีสารสนเทศ ห้อง Audi",time:"9.00-12.00",date:"จ.",image:[{no1:"https://www.techtalkthai.com/wp-content/uploads/2016/11/kmitl_it_data_science_01.jpg",no2:"https://www.it.kmitl.ac.th/wp-content/themes/itkmitl2017wp/img/life/life-10.jpg"}],route:"https://g.page/ITKMITL?share",email:"nopporn@it.kmitl.ac.th"},
        {id:"06016309",name:"INFORMATION SYSTEM SECURITY AND IT LAWS",credit:"3",teach:"ผศ.ดร. สุเมธ ประภาวัต",room:"ตึก IT คณะเทคโนโลยีสารสนเทศ ห้อง M23",time:"9.00-13.00",date:"อ.",image:[{no1:"https://www.techtalkthai.com/wp-content/uploads/2016/11/kmitl_it_data_science_01.jpg",no2:"https://fastly.4sqi.net/img/general/699x268/1TFE4JRX1R04XIRHVCQL52PVR2J4XUTYBLKOADQPFJMP3ZI2.jpg"}],route:"https://g.page/ITKMITL?share",email:"sumet@it.kmitl.ac.th"},
        {id:"06016319",name:"INTRODUCTION TO COMPUTER SYSYEMS",credit:"3",teach:"ผศ.ดร. สุภกิจ นุตยะสกุล",room:"ตึก IT คณะเทคโนโลยีสารสนเทศ ห้อง PROJECT BASE ชั้น 3",time:"13.00-16.00",date:"พ.",image:[{no1:"https://www.techtalkthai.com/wp-content/uploads/2016/11/kmitl_it_data_science_01.jpg",no2:"https://static.trueplookpanya.com/tppy/member/m_525000_527500/525016/cms/images/%E0%B8%9E%E0%B8%B5%E0%B9%88%E0%B8%AB%E0%B8%A2%E0%B8%B2%E0%B8%87%20%E0%B8%A0%E0%B8%B2%E0%B8%9E%E0%B8%9B%E0%B8%A3%E0%B8%B0%E0%B8%81%E0%B8%AD%E0%B8%9A%20%E0%B8%9A%E0%B8%A3%E0%B8%A3%E0%B8%A2%E0%B8%B2%E0%B8%81%E0%B8%B2%E0%B8%A8%E0%B9%83%E0%B8%99%E0%B8%AB%E0%B9%89%E0%B8%AD%E0%B8%87%E0%B9%80%E0%B8%A3%E0%B8%B5%E0%B8%A2%E0%B8%99%20(4).png"}],route:"https://g.page/ITKMITL?share",email:"supakit@it.kmitl.ac.th"},
        {id:"06016323",name:"MOBILE DEVICE PROGRAMMING",credit:"3",teach:"ดร. พัฒนพงษ์ ฉันทมิตรโอภาส",room:"ตึก IT คณะเทคโนโลยีสารสนเทศ ห้อง L207",time:"14.00-18.00",date:"อ.",image:[{no1:"https://www.techtalkthai.com/wp-content/uploads/2016/11/kmitl_it_data_science_01.jpg",no2:"https://www.kmitl.ac.th/sites/default/files/2022-11/55.1.jpg"}],route:"https://g.page/ITKMITL?share",email:"pattanapong@it.kmitl.ac.th"},
      ],
      
      mySubject:[

        {id:"06016310",name:"HUMAN INTERFACE DESIGN",credit:"3",teach:"รศ.ดร.นพพร โชติกกำธร",room:"ตึก IT คณะเทคโนโลยีสารสนเทศ ห้อง Audi",time:"9.00-12.00",date:"จ.",image:[{no1:"https://www.techtalkthai.com/wp-content/uploads/2016/11/kmitl_it_data_science_01.jpg",no2:"https://www.it.kmitl.ac.th/wp-content/themes/itkmitl2017wp/img/life/life-10.jpg"}],route:"https://g.page/ITKMITL?share",email:"nopporn@it.kmitl.ac.th"},       
        {id:"06016323",name:"MOBILE DEVICE PROGRAMMING",credit:"3",teach:"ดร. พัฒนพงษ์ ฉันทมิตรโอภาส",room:"ตึก IT คณะเทคโนโลยีสารสนเทศ ห้อง L207",time:"14.00-18.00",date:"อ.",image:[{no1:"https://www.techtalkthai.com/wp-content/uploads/2016/11/kmitl_it_data_science_01.jpg",no2:"https://www.kmitl.ac.th/sites/default/files/2022-11/55.1.jpg"}],route:"https://g.page/ITKMITL?share",email:"pattanapong@it.kmitl.ac.th"},     
        ],
      idSubject:"",
      modalAddSubject:false,
      modalShowDetail:false,
      selectSubject:[],
      search:"",
      showMySubject:[],
      modalDelete:false,
      indexDelete:'',
    };
  },
  mounted() {
    // this.getNovels();
    // this.getShelfBooks();
    this.showSeach();
  },
  methods: {  
    addMySubject(){
      console.log("AddSubject")
 
      let addS = this.subject.filter((val)=>(val.id ==this.idSubject))
      let myS = this.mySubject.filter((val)=>(this.idSubject ==val.id))
      console.log(addS[0])
      console.log(myS)
      if(this.idSubject!==""){

        if(myS.length<=0){
          this.mySubject.push(addS[0]);
          this.showMySubject = this.mySubject
          this.modalAddSubject = false;
        }
        else{
          alert("คุณได้เพิ่มวิชานี้ในชั้นเรียนแล้ว")
        }
      }
      else{
        this.modalAddSubject = false
      }
  
    },
    showDetail(id){
      this.modalShowDetail = true;
      this.selectSubject = this.mySubject.filter((val)=>(id==val.id))
    },
    showSeach(){
      if(this.search==''){
        this.showMySubject=this.mySubject
      }
      else{
        this.showMySubject=this.mySubject.filter((val)=>(val.id.includes(this.search) || val.name.includes(this.search.toUpperCase())))
      }
    },

    linktoNews(id,mySubject){
      this.$router.push({ name: 'news2', params: { idSubject:id ,name:mySubject.name,teach:mySubject.teach}})
    },
    deleteSubject_my(id,index){
      this.modalDelete = true;
      this.selectSubject = this.mySubject.filter((val)=>(id==val.id));
      this.indexDelete = index;
    },
    confirmDelete(){
      this.mySubject.splice(this.indexDelete,1)
      this.modalDelete = false
    }


  },
};
</script>
