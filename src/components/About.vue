<template>
  <div class="about-page page">
    <template v-for="section in sections">
      <div v-on:click="resize" class="col" ref="section" v-bind:class="{focus:section.focus, equal:section.equal, minor:section.minor, aboutCol:section.about, thinkCol:section.think, designCol:section.design, buildCol:section.build}">
        <div v-bind:class="{about:section.about, think:section.think, design:section.design, build:section.build, background:section.focus}">
          <transition name="appear"><h1 v-show="section.focus">{{section.title}}</h1></transition>
          <transition name="appear"><p v-show="section.focus">{{section.paragraph}}</p></transition>
        </div>
      </div>
    </template>

  </div>
</template>

<script>
import {bus} from "../main"

export default {

  data() {
    return {
      refs: ["col1", "col2", "col3", "col4"],
      sections: [
        { title:"About", ref:"col1", background:'require think.png',
         paragraph:"Pinsapo is a web development company created by me, Gregory Barrett. I create, design and develop bespoke web apps for all kinds of businesses. My expertise lie in Rails and Vue, utilising the best bits of each of them to make seamless apps which are both functional and intuitive.", focus:false, equal:true, minor:false, about:true },
        { title:"Think", ref:"col2", background:"url(../assets/think.png)", paragraph:"No one knows your product or service better than you. But the thought of building a website probably leaves your head spinning. Together, we will find the best way to showcase your business online whilst letting me take care of all the technical details.", focus:false, equal:true, minor:false, think:true },
        { title:"Design", ref:"col3", background:"url(../assets/design.png)", paragraph:"Your business is unique and therefore needs a totally bespoke design. By tailoring colours, fonts, transitions and images we will create your online presence without the constraints of conventional templates.", focus:false, equal:true, minor:false, design:true },
        { title:"Build", ref:"col4", background:"url(../assets/build.png)", paragraph:"It's over to us for this stage. Your ideas will be turned into reality using the most up to date technologies and tools. Testing along the way will ensure you receive a fully functioning, future proof site, ready for everything the real world throws at it.", focus:false, equal:true, minor:false, build:true }
      ]//sections
    }//return
  },//data
  methods: {
    resize(e) {
      for (var i=0; i<= this.refs.length-1; i++) {
        if (this.$refs.section[i] === e.currentTarget) {
          //if clicked add focus class and remove others
          this.sections[i].focus=true;
          this.sections[i].minor=false;
        } else {
          //if not clciked add minor class
          this.sections[i].focus=false;
          this.sections[i].minor=true;
        }//if
        //after click event non are equal
        this.sections[i].equal=false;
      }//for
    }//resize
  },//methods
  created() {
    bus.$emit('pageChange', 1)
  }
}
</script>


<style scoped lang="scss">
.about-page {
  width: 100%;
  height: 100%;
  position: fixed;

}
.page {
  font-family: 'Open Sans', sans-serif;

}

.col {
  float: left;
  height: 100%;
  transition: width 1s;
}

.about {
  background-image: url(../assets/about-long.png);
  background-position: top;
  background-size: contain;
  background-repeat: no-repeat;
  height: 100%;
}
.think {
  background-image: url(../assets/think-long.png);
  background-position: top;
  background-size: contain;
  background-repeat: no-repeat;
  height: 100%;
}

.design {
  background-image: url(../assets/design-long.png);
  background-position: top;
  background-size: contain;
  background-repeat: no-repeat;
  height: 100%;
}
.build {
  background-image: url(../assets/build-long.png);
  background-position: top;
  background-size: contain;
  background-repeat: no-repeat;
  height: 100%;

}
.focus {
 width:85%;
}
.equal {
  width: 25%;
  transition: opacity .5s;
}

.minor {
  width: 5%;
}
.equal:hover, .minor:hover {
  opacity: .8;

}
.background {
  background: none;
}

.aboutCol {
  background-color: #16235a;
  color: #F3F3F2;
}
.thinkCol {
  background-color: #F3F3F2;
  color: #16235a;
}
.designCol {
  background-color: #16235a;
  color: #F3F3F2;
}
.buildCol {
  background-color: #F3F3F2;
  color: #16235a;
}

//transitions for the paragraph
.appear-enter-active {
  transition: opacity 1s ease-out 2s;

}
.appear-leave-active {
  transition: opacity 0s ease-out;
}
.appear-enter, .appear-leave-to {
  opacity:0;
}

h1 {
  font-size: 3.5em;
  position: relative;
  top: 10vw;
  left: 10vw;
}
p {
  left: 10vw;
  font-size: 1.8em;
  line-height: 1.4em;
  position: relative;
  top: 12vw;
  width: 30%;
}


@media only screen and (max-width: 1024px) {
  p {
    width: 60%;
  }
}
@media only screen and (max-width: 812px) {

  h1 {
    font-size: 3.5em;
    position: relative;
    top: 3vw;
    left: 3vw;
  }
  p {
    left: 3vw;
    font-size: 1.8em;
    line-height: 1.4em;
    position: relative;
    top: 6vw;
    width: 80%;
  }
}
@media only screen and (max-width: 768px) {

  .col {
    //width: 100vw;
    //height: 25vh;
    transition: height 2s;
    width: 100%;
    height: 25%;

  }
  .focus {
    //height:85vh;
    height:85%;
    overflow: auto;
  }
  .equal {
    //height: 25vh;
    height: 25%;
  }
  .minor {
    //height: 5vh;
    height: 5%;
  }
  .about {
    background-image: url(../assets/about-lat.png);
    background-position:center;
  }
  .think {
    background-image: url(../assets/think-lat.png);
    background-position:center;

  }
  .design {
    background-image: url(../assets/design-lat.png);
    background-position:center;
  }
  .build {
    background-image: url(../assets/build-lat.png);
    background-position:center;
  }
  .background {
    background: none;
    position: relative;
    overflow: hidden;
  }

  h1 {
    font-size: 3.5em;
    position: relative;
    top: 8vh;
    left: 8vw;
  }
  p {
    left: 8vw;
    font-size: 1.8em;
    line-height: 1.4em;
    position: relative;
    top: 12vh;
    width: 80%;
  }
}

@media only screen and (max-width: 568px) {
  h1 {
    font-size: 2.5em;
    top: 3vh;
    left: 40px;
  }
  p {
    left: 40px;
    font-size: 1.5em;
    line-height: 1.4em;
    top: 6vh;
    width: 80%;
  }
}
</style>
