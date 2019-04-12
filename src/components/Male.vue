<template lang="html">
  <div class="container">
    <div v-if="won" id='grey'></div>
    <div v-if="won" id='wonnn'>
      <img src="https://i.imgur.com/iyIegyd.png" alt="">
    </div>
    <div class="modal animated fadeInDown" id='modal' v-bind:class="{'is-active' : error.length > 1}">
      <div class="box" id='width'>
        <article class="media">
          <div class="media-left">
            <figure class="image is-64x64">
              <img src="http://www.gstatic.com/tv/thumb/persons/589228/589228_v9_ba.jpg" alt="Image">
            </figure>
          </div>
          <div class="media-content">
            <div class="content">
              <button @click='closeModal' class="delete is-pulled-right" aria-label="close"></button>
              <p>
                <strong>Mark Zuckerberg</strong> <small class="has-text-info"><a href="https://www.facebook.com/zuck" target='_blank'>@markzuckerberg</a></small>
                <br><br>
                {{ error }}
              </p>
            </div>
          </div>
        </article>
      </div>
    </div>
    <div class="panel">
      <p class="panel-heading has-text-primary has-background-link">
        <span class="is-pulled-left is-size-6"><a href="." class="has-text-white">◄ Go Back</a></span>
        <span class="has-text-white">{{ name }}</span>
        <span class="is-pulled-right is-size-5 has-text-white">Θ</span>
      </p>
      <div id='box'>
        <div v-for='message in messages' v-bind:key='message.id' class="space">
          <span v-if='message.id == 1' style="max-width:70%">
            <figure class="image is-24x24 is-pulled-left" style="margin-top:15px; margin-right:5px; margin-left:7px">
              <img class="is-rounded" src="https://i2-prod.mirror.co.uk/incoming/article9945877.ece/ALTERNATES/s615/MAIN-MSP_MDG_010317Jenner_821JPG.jpg" alt="Image">
            </figure>
            <span class="has-text-light is-pulled-left pcmessage">{{ message.message }}</span>
          </span>
          <span v-else class="is-pulled-right usermessage" style="max-width:70%">{{ message }}</span>
        </div>
      </div>
      <div id="seen">
        <span v-if='seen' class="is-pulled-right has-text-grey-light" style="margin-right:2rem">{{ time }}</span>
        <span v-if='typing' class="is-pulled-left has-text-grey-light" style="margin-left:2rem">typing ...</span>
      </div>
      <div v-if='restart' class="panel-block margin-10">
        <button @click='restartGame' class="button is-dark" style="min-width:90%; margin:0 5%">Restart</button>
      </div>
      <div v-else class="panel-block" id="display-block">
        <button v-for='buttonMessage in buttonMessages' @click='value(buttonMessage.message,buttonMessage.value)' @key='buttonMessage.value' v-bind:class="{'button is-loading' : loading}" :value='buttonMessage.value' id="buttonText">{{ buttonMessage.message }}</button>
      </div>
      {{ counter }}
      {{ level }}
    </div>
  </div>
</template>

<script>
export default {
  props : {
    name : {
      type: String
    }
  },
  data() {
    return {
      messages : [],
      buttonMessages : [
        {
          value: 1 ,
          message : 'nuk ka perfundu'
        },
        {
          value: 2 ,
          message : 'eksperiment'
        },{
          value: 3 ,
          message : 'thjesht logjika jo teksti'
        }
      ],
      loading : false,
      counter : 0,
      level : 1,
      error : '',
      won: false,
      restart : false,
      seen : false,
      typing : false,
      time : ''
    }
  },
  methods : {
    value(m,v) {
      this.messages.push(m);
      this.counter += v;
      this.scroll = setTimeout(() => {
        //scroll
        let elem = document.querySelector('#box');
        elem.scrollTo(0,elem.scrollHeight);
        this.loading = true;
      }, 1);

      //msg 1
      if (this.level == 1 && (v == 1 || v == 3)) {
        this.add = setTimeout(() => {
          this.seen = true;
          this.time = `✔ seen `+ new Date().toLocaleTimeString();
        }, 1000);
        this.add = setTimeout(() => {
          this.typing = true;
          this.seen = false;
        }, 2000);
        this.add = setTimeout(() => {
          this.scroll = setTimeout(() => {
            //scroll
            let elem = document.querySelector('#box');
            elem.scrollTo(0,elem.scrollHeight);
          }, 1);
          this.messages.push({id:1, message:'Cili ekip o ma i miri ?'});
          this.loading = false;
          this.level = this.level + 1 ;
          this.typing = false;
          if (this.level == 2) {
            this.buttonMessages = [{
              value: 1 ,
              message : 'Bayern'
            },
            {
              value: 2 ,
              message : 'Ac Milan'
            },{
              value: 3 ,
              message : 'Real'
            }];
          }
        }, 4000);
      } else if( this.level == 1 && v == 2) {
        this.add = setTimeout(() => {
            this.seen = true;
            this.time = `✔ seen `+ new Date().toLocaleTimeString();
        }, 1000);
        this.err = setTimeout(() => {
          this.error = "Don't text you back.";
          this.loading = true;
          this.restart = true;
          this.seen = true;
        }, 3000);
      }

      //msg 2
      if (this.restart == false) {
        if (this.level == 2 && (v == 1 || v == 3)) {
          this.add = setTimeout(() => {
              this.seen = true;
              this.time = `✔ seen `+ new Date().toLocaleTimeString();
          }, 1000);
          this.err = setTimeout(() => {
            this.error = "No he is not.";
            this.loading = true;
            this.restart = true;
          }, 4000);
        } else if(this.level == 2 && v == 2) {
          this.add = setTimeout(() => {
              this.seen = true;
              this.time = `✔ seen `+ new Date().toLocaleTimeString();
          }, 1500);
          this.add = setTimeout(() => {
            this.typing = true;
            this.seen = false;
          }, 2000);
          this.add = setTimeout(() => {
            this.scroll = setTimeout(() => {
              //scroll
              let elem = document.querySelector('#box');
              elem.scrollTo(0,elem.scrollHeight);
            }, 1);
            this.messages.push({id:1, message:'Kush i ka 7 ch.league ?'});
            this.loading = false;
            this.level = this.level + 1 ;
            this.typing = false;
            if (this.level == 3) {
              this.buttonMessages = [{
                value: 1 ,
                message : 'Ac Milan'
              },
              {
                value: 2 ,
                message : 'Bayern'
              },{
                value: 3 ,
                message : 'Real'
              }];
            }
          }, 5000);
        }
      }

      //msg 3
      if (this.restart == false) {
        if (this.level == 3 && (v == 2 || v == 3)) {
          this.add = setTimeout(() => {
              this.seen = true;
              this.time = `✔ seen `+ new Date().toLocaleTimeString();
          }, 1000);
          this.err = setTimeout(() => {
            this.error = "No he is not.3";
            this.loading = true;
            this.restart = true;
          }, 2000);
        } else if(this.level == 3 && v == 1) {
          this.add = setTimeout(() => {
              this.seen = true;
              this.time = `✔ seen `+ new Date().toLocaleTimeString();
          }, 1700);
          this.add = setTimeout(() => {
            this.typing = true;
            this.seen = false;
          }, 4000);
          this.add = setTimeout(() => {
            this.scroll = setTimeout(() => {
              //scroll
              let elem = document.querySelector('#box');
              elem.scrollTo(0,elem.scrollHeight);
            }, 1);
            this.messages.push({id:1, message:'Nickname ?'});
            this.loading = false;
            this.level = this.level + 1 ;
            this.typing = false ;
            if (this.level == 4) {
              this.buttonMessages = [{
                value: 1 ,
                message : 'G-eat'
              },
              {
                value: 2 ,
                message : 'Geat'
              },{
                value: 3 ,
                message : 'GG'
              }];
            }
          }, 7500);
        }
      }

      //msg 4
      if (this.restart == false) {
        if (this.level == 4 && v == 3) {
          this.add = setTimeout(() => {
              this.seen = true;
              this.time = `✔ seen `+ new Date().toLocaleTimeString();
          }, 1000);
          this.err = setTimeout(() => {
            this.error = "No he is not my Nickname.4";
            this.loading = true;
            this.restart = true;
          }, 2000);
        } else if(this.level == 4 && (v == 1 || v == 2)) {
          this.add = setTimeout(() => {
              this.seen = true;
              this.time = `✔ seen `+ new Date().toLocaleTimeString();
          }, 7000);
          this.add = setTimeout(() => {
            this.typing = true;
            this.seen = false;
          }, 15000);
          this.add = setTimeout(() => {
            this.typing = false;
          }, 30000);
          this.add = setTimeout(() => {
            this.typing = true;
          }, 35000);
          this.add = setTimeout(() => {
            this.scroll = setTimeout(() => {
              //scroll
              let elem = document.querySelector('#box');
              elem.scrollTo(0,elem.scrollHeight);
            }, 1);
            this.messages.push({id:1, message:'Say Hello ?'});
            this.loading = false;
            this.level = this.level + 1 ;
            this.typing = false ;
            if (this.level == 5) {
              this.buttonMessages = [{
                value: 1 ,
                message : 'hello'
              },
              {
                value: 2 ,
                message : 'hellO'
              },{
                value: 3 ,
                message : 'Hello'
              }];
            }
          }, 40000);
        }
      }

      //msg 5
      if (this.restart == false) {
        if (this.level == 5 && (v == 1 || v == 2)) {
          this.add = setTimeout(() => {
              this.seen = true;
              this.time = `✔ seen `+ new Date().toLocaleTimeString();
          }, 1000);
          this.err = setTimeout(() => {
            this.error = "No he is not my Hello.5";
            this.loading = true;
            this.restart = true;
          }, 4000);
        } else if(this.level == 5 && v == 3) {
          this.add = setTimeout(() => {
              this.seen = true;
              this.time = `✔ seen `+ new Date().toLocaleTimeString();
          }, 2000);
          this.add = setTimeout(() => {
            this.typing = true;
            this.seen = false;
          }, 15000);
          this.add = setTimeout(() => {
            this.scroll = setTimeout(() => {
              //scroll
              let elem = document.querySelector('#box');
              elem.scrollTo(0,elem.scrollHeight);
            }, 1);
            this.messages.push({id:1, message:'nothing'});
            this.loading = false;
            this.level = this.level + 1 ;
            this.typing = false ;
            if (this.level == 6) {
              this.buttonMessages = [{
                value: 1 ,
                message : 'ok'
              },
              {
                value: 2 ,
                message : 'nah'
              },{
                value: 3 ,
                message : 'ninonona'
              }];
            }
          }, 20000);
        }
      }

      //msg 6
      if (this.restart == false) {
        if (this.level == 6 && this.counter > 10) {
          this.add = setTimeout(() => {
              this.seen = true;
              this.time = `✔ seen `+ new Date().toLocaleTimeString();
          }, 5000);
          this.add = setTimeout(() => {
            this.typing = true;
            this.seen = false;
          }, 10000);
          this.add = setTimeout(() => {
            this.typing = false;
          }, 16000);
          this.add = setTimeout(() => {
            this.typing = true;
          }, 22000);
          this.add = setTimeout(() => {
            this.scroll = setTimeout(() => {
              //scroll
              let elem = document.querySelector('#box');
              elem.scrollTo(0,elem.scrollHeight);
            }, 1);
            this.messages.push({id:1, message:'Q.6'});
            this.loading = false;
            this.level = this.level + 1 ;
            this.typing = false ;
            if (this.level == 7) {
              this.buttonMessages = [{
                value: 1 ,
                message : 'no 7'
              },
              {
                value: 2 ,
                message : 'Yes'
              },{
                value: 3 ,
                message : 'Idon\'t know'
              }];
            }
          }, 27000);
      } else if (this.level >= 6 && this.counter <= 10){
        this.add = setTimeout(() => {
            this.seen = true;
            this.time = `✔ seen `+ new Date().toLocaleTimeString();
        }, 1000);
        this.addError = setTimeout(() => {
          this.error = 'EEEEEEEEEEEEEEEEEEErrrrrrrrrrrrorrrrr';
        }, 1001);
        this.restart = true;
      }
    }

    //msg 7
    if (this.restart == false) {
      if (this.level == 7 && (v == 1 || v == 3)) {
        this.add = setTimeout(() => {
            this.seen = true;
            this.time = `✔ seen `+ new Date().toLocaleTimeString();
        }, 1000);
        this.err = setTimeout(() => {
          this.error = "No he is not my Hello.7";
          this.loading = true;
          this.restart = true;
        }, 1500);
      } else if(this.level == 7 && v == 2) {
        this.add = setTimeout(() => {
            this.seen = true;
            this.time = `✔ seen `+ new Date().toLocaleTimeString();
        }, 1000);
        this.add = setTimeout(() => {
          this.typing = true;
          this.seen = false;
        }, 1500);
        this.add = setTimeout(() => {
          this.typing = false;
        }, 2000);
        this.add = setTimeout(() => {
          this.typing = true;
        }, 2500);
        this.add = setTimeout(() => {
          this.scroll = setTimeout(() => {
            //scroll
            let elem = document.querySelector('#box');
            elem.scrollTo(0,elem.scrollHeight);
          }, 1);
          this.messages.push({id:1, message:'7777'});
          this.loading = false;
          this.level = this.level + 1 ;
          this.typing = false;
          if (this.level == 8) {
            this.buttonMessages = [{
              value: 1 ,
              message : '4-7'
            },
            {
              value: 2 ,
              message : '4*7'
            },{
              value: 3 ,
              message : '4+7'
            }];
          }
        }, 7000);
      }
    }

    //msg 8
    if (this.restart == false) {
      if (this.level == 8 && v == 2) {
        this.add = setTimeout(() => {
            this.seen = true;
            this.time = `✔ seen `+ new Date().toLocaleTimeString();
        }, 1000);
        this.err = setTimeout(() => {
          this.error = "No he is not my Hello.8";
          this.loading = true;
          this.restart = true;
        }, 3000);
      } else if(this.level == 8 && (v == 1 || v == 3)) {
        this.add = setTimeout(() => {
            this.seen = true;
            this.time = `✔ seen `+ new Date().toLocaleTimeString();
        }, 1000);
        this.add = setTimeout(() => {
          this.typing = true;
          this.seen = false;
        }, 1500);
        this.add = setTimeout(() => {
          this.scroll = setTimeout(() => {
            //scroll
            let elem = document.querySelector('#box');
            elem.scrollTo(0,elem.scrollHeight);
          }, 1);
          this.messages.push({id:1, message:'Ora ?'});
          this.loading = false;
          this.level = this.level + 1 ;
          this.typing = false;
          if (this.level == 9) {
            this.buttonMessages = [{
              value: 1 ,
              message : '2:31'
            },
            {
              value: 2 ,
              message : '2:31 PM'
            },{
              value: 3 ,
              message : '14:31'
            }];
          }
        }, 3000);
      }
    }

    //msg 9
    if (this.restart == false) {
      if (this.level == 9 && (v == 2 || v == 3)) {
        this.add = setTimeout(() => {
            this.seen = true;
            this.time = `✔ seen `+ new Date().toLocaleTimeString();
        }, 1000);
        this.err = setTimeout(() => {
          this.error = "No he is not my q.9.9";
          this.loading = true;
          this.restart = true;
        }, 2000);
      } else if(this.level == 9 && v == 1) {
        this.add = setTimeout(() => {
            this.seen = true;
            this.time = `✔ seen `+ new Date().toLocaleTimeString();
        }, 1000);
        this.add = setTimeout(() => {
          this.typing = true;
          this.seen = false;
        }, 5000);
        this.add = setTimeout(() => {
          this.scroll = setTimeout(() => {
            //scroll
            let elem = document.querySelector('#box');
            elem.scrollTo(0,elem.scrollHeight);
          }, 1);
          this.messages.push({id:1, message:'DDDasd ?'});
          this.loading = false;
          this.level = this.level + 1 ;
          this.typing = false;
          if (this.level == 10) {
            this.buttonMessages = [{
              value: 1 ,
              message : 'GAti Finish'
            },
            {
              value: 2 ,
              message : 'Finish'
            },{
              value: 3 ,
              message : 'I Wonnnn'
            }];
          }
        }, 14000);
      }
    }

    //msg 10
    if (this.restart == false) {
      if (this.level == 10 && (v == 1 || v == 2)) {
        this.add = setTimeout(() => {
            this.seen = true;
            this.time = `✔ seen `+ new Date().toLocaleTimeString();
        }, 1000);
        this.err = setTimeout(() => {
          this.error = "Soo Closeeee !";
          this.loading = true;
          this.restart = true;
        }, 1500);
      } else if(this.level == 10 && v == 3) {
        this.add = setTimeout(() => {
            this.seen = true;
            this.time = `✔ seen `+ new Date().toLocaleTimeString();
        }, 1000);
        this.add = setTimeout(() => {
          this.scroll = setTimeout(() => {
            //scroll
            let elem = document.querySelector('#box');
            elem.scrollTo(0,elem.scrollHeight);
          }, 1);
          this.messages.push({id:1, message:'See You Tonight.'});
          this.loading = false;
          this.error = 'Youuuu Winnnn';
          this.won = true;
          this.restart = true;
        }, 4000);
      }
    }


      //scroll
      this.scroll = setTimeout(() => {
        let elem = document.querySelector('#box');
        elem.scrollTo(0,elem.scrollHeight);
      }, 1);
    },
    closeModal() {
      this.error = '';
      this.loading = false;
    },
    restartGame(){
      this.messages = [];
      this.buttonMessages = [
        {
          value: 1 ,
          message : 'Hello'
        },
        {
          value: 2 ,
          message : 'Tung'
        },{
          value: 3 ,
          message : 'Hi'
        }
      ];
      this.loading = false;
      this.counter = 0;
      this.level = 1;
      this.error = '';
      this.restart = false;
      this.won = false;
      this.seen = false;
    }
  }
}
</script>

<style lang="css" scoped>
  .space {
    height: 3rem;
  }

  #grey {
    position: fixed;
    height: 100%;
    top: 0;
    right: 0;
    left: 0;
    background: rgba(213, 218, 226, 0.9);
  }

  #box {
    height: 30rem;
    margin: 0;
    overflow: auto;
    border-right: 1px solid #dfdfdf;
    border-left: 1px solid #dfdfdf;
  }

  #seen {
    height: 2rem;
    border-right: 1px solid #dfdfdf;
    border-left: 1px solid #dfdfdf;
    border-bottom: 1px solid #dfdfdf;
  }

  .pcmessage {
    background: hsl(217, 71%, 53%);
    padding: 0.5rem 1.5rem;
    margin : 5px 1rem 5px 0;
    border-radius: 25px;
  }

  .usermessage {
    background: hsl(0, 0%, 86%);
    padding: 0.5rem 1.5rem;
    margin : 5px 1rem;
    border-radius: 25px;
  }

  #modal {
    justify-content: flex-start;
  }

  #width {
    width: 100%;
  }

  #wonnn {
    position: absolute;
    top: 25vh;
  }

  /* #buttonText {
    white-space: wrap !important;
    background: hsl(204, 86%, 53%);
    color: white;
    padding: 0.2rem;
    height: auto;
  } */

  #buttonText {
    font-weight:400;
    color:#eaf1fc;
    background: hsl(204, 86%, 53%);
    width: 32% ;
    margin-right: 2%;
    white-space:wrap;
    vertical-align:middle;
    border:1px solid transparent;
    padding:.375rem .75rem;
    font-size:1rem;
    line-height:1.5;
    border-radius:.25rem;
    transition:color .15s ease-in-out,background-color .15s ease-in-out,border-color .15s ease-in-out,box-shadow .15s ease-in-out;
  }

  #buttonText:hover {
    background-color:#0069d9;
    border-color:#0062cc;
  }

  @media only screen and (max-width: 600px) {
    .usermessage {
      font-size: 0.8rem;
      padding: 0.4rem 1.1rem;
    }

    .pcmessage {
      font-size: 0.8rem;
      padding: 0.4rem 1.1rem;
    }
  }

  @media only screen and (max-width: 950px) {
      #display-block {
        display: block;
      }

      #display-block #buttonText{
        display: block;
        width: 100%;
        margin-bottom: 0.2rem;
      }
  }

  @media only screen and (max-height: 700px) {
      #box{
        height: 18rem;
      }
  }
</style>
