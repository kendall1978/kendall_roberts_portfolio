<template>
<div>
  <!-- Rounded Circle Card -->
  <b-card-group class="roundContainer justify-content-center">
    <b-row>
      <b-col class="col-12 col-lg-6">
        <b-card no-body class="text-center">
          <b-card-img :src="mugShot.img"  
          class="rounded-circle"></b-card-img>
        </b-card>
      </b-col>
      <!-- Title Card -->
      <b-col class="col-12 col-lg-6">
        <b-card class="text-center" id="titleCard" >
          <h4>Kendall Roberts</h4>
            <b-card-text style="background-color: rgb(131,131,131);">
              Web-Developer, Student, and Part-Time Dad Joke Comedian
            </b-card-text>
        </b-card>
        <!-- Font awesome links -->
        <b-card>
          <a href="https://github.com/kendall1978?tab=repositories"><i class="fab fa-github"></i></a>
          <a href="https://www.linkedin.com/in/kendall-roberts-1b8b3a171/"><i class="fab fa-linkedin"></i></a>
          <a href="https://twitter.com/kendertsrondall"><i class="fab fa-twitter"></i></a>
          <a href="https://www.instagram.com/kendall_roberts49/"><i class="fab fa-instagram"></i></a>
        </b-card>
      </b-col>
    </b-row>
  </b-card-group>
  <!-- for loop for my small amount of json -->
  <div class="newContain">
      <div v-for="card in cardContent" :key="card.id">
        <b-col>
          <b-card align="left" class="newBox">
            <div class="cardContent">
              <h4>{{card.title}}</h4>
              <b-card-text>
                {{card.content}}
              </b-card-text>
            </div>
          </b-card>
        </b-col>
      </div>
  </div>
</div>
</template>

<script>
import firebase from "firebase"; 

export default {
  name: 'home',
  data(){
    // Returning my images to be usable as well as laying out my json.
      return{
        mugShot: "",
        cardContent: [{
          id: 1,
          title: "My Education",
          content: "I've been interested in technology and code since I was in high school. My first project-setting me up to love this field-was putting RetroPie on a Raspberry Pi. Ever since then I've loved this field. So I went to Ozarks Technical Community College and finished a degree in Computer Information Science"
          },
          {
            id: 2,
            title: "My Life",
            content: "Nerd for life, I love work on a computer and write code. I also find enjoyment in activities like fishing, hunting, hiking, and boating. Put me in a kayak on a river somewhere and I am one happy guy."
          },
          {
            id: 3,
            title: "My Future",
            content: "My long term goal is to be a well respected full stack software engineer with a project manager role in mind. My short term goals are always to continue to challege myself with new technologies and write quality code. At the end of the day I just want to learn all that I can about web development."
          }
          
        ]
      }
  },
  created(){
      const ref = firebase.firestore().collection('assets').doc('homePic')
      ref.get()
      .then(snapshot => {
        console.log(snapshot.data)
          if(snapshot.exists){
            this.mugShot = snapshot.data()
          }else{
            console.log('Doesnt exist')
          }
      })

  },
  methods: {
  },

  props: {}
}
</script>


<style scoped>

*{
  margin: 0;
  padding: 0;
  box-sizing: border-box;
  color:rgb(36, 37, 39);
  background: rgb(36, 37, 39);

}

/* Font awesome icons */
.fab, .fas{
  font-size: 5em;
  padding: 20px;
  transition: all 300ms ease-in;
  color: rgb(131, 131, 131);


}


.fas:hover, .fab:hover{
  color: #E07A5F;
}

/* Rounded card properties */

.roundContainer{
  width: 100%;
  height: 80%;

  
}

.roundContainer .card{
  width: 100%;
  background-color: rgb(36, 37, 39);  
  border: none; 
  margin: 50px auto;
  text-align: center;
}

.rounded-circle{
  transition: all 350ms ease-in;
  box-shadow: 10px 10px 12px 0 rgba(0, 0, 0, 0.5) ;
  
}

/* title card next to or below round card */


#titleCard{
  width: 80%;
  border-radius: 10px;
  border: none;
  padding: 20px 17px;
  box-shadow: 10px 10px 12px 0 rgba(0, 0, 0, .7),
  -10px -10px 14px 0 rgba(78, 78, 78, 0.548) ;
  background: rgb(131, 131, 131);
  
}
#titleCard h4{
  color:rgb(36, 37, 39);
  background: rgb(131, 131, 131);
}

.rounded-circle:hover{
  transform: translateY(-20px);
  
}



.rounded-circle {
  width: 80%; 
  margin-left: 10%;
}
/* Experiments with new card styles */

.newContain{
  width: 100%;
  height: auto;
  display: flex;
  justify-content: space-evenly;
  align-items: flex-start;
  flex-wrap: wrap;
  padding: 60px 0;
  
  
}

.newBox{
  padding: 1.75px .5px;
  transition: all 400ms ease-in-out;
  z-index: 1;
  width: 450px;
  height: 475px;
  margin: 30px 20px;
 
} 



 .newContain .newBox::before{
  content: '';
  position: absolute;
  top: 0px;
  left: 0px;
  right: 0px;
  bottom: 0px;
  padding: 5px;
  border: none;
  border-radius: 8px;
  transform: skew(1.7deg, 1.7deg);
  background: linear-gradient(300deg, #E07A5F, #81B29A);
  z-index: -1;
  box-shadow: 10px 10px 12px 0 rgba(0, 0, 0, 0.5),
  -10px -10px 14px 0 rgba(78, 78, 78, 0.548)  ;
  
}

.cardContent{
  height: 100%;
  width: 100%;
  padding: 15px 20px;
  
  border-radius: 0 8px 0 8px;
  background: rgb(131, 131, 131);
  

}

.newBox .cardContent p{
  font-size: 1.25em;
  padding: 10px 15px;
  color: rgb(36, 37, 39);
  background: rgb(131, 131, 131); 
}

.newBox .cardContent h4{
  font-size: 3em;
  padding: 10px 5px;
  opacity: .8;
  transition: all 350ms ease-in;
  color: rgb(36, 37, 39);
  background: rgb(131, 131, 131); 
}

.newBox:hover .cardContent h4{
  transform: translateX(20px);
}

.newBox:hover{
  transform: translateY(-10px);
}

@media only screen and (max-width: 800px){
   .newBox:hover{
    transform: none;
  }
  .newBox:hover .cardContent h4{
    transform: none;
  }

  .rounded-circle:hover{
  transform: none;
  
}
}

@media only screen and (max-width: 550px) {
  .newBox{
    width:350px;
    height: 375px;
    margin: 30px 20px;
  }
  
  .newBox .cardContent p {
    font-size: .95em;
  }
  .newBox .cardContent h4 {
    font-size: 2em;
  }

 
}

@media only screen and (max-width: 400px){
  .newBox{
    width: 300px;
    height: 325px;
  }
  .newBox .cardContent p {
    font-size: .85em;
  }
  .newBox .cardContent h4 {
    font-size: 1.75em;
  }
}





.card p{
  font-size: 18px;
}
</style>