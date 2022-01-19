<template>
  <div class="wait-list">
    <div class="wait-list-col">     
      <div class="left">
        <div class="left-top">
          <img
              src="assets/images/logo.jpg"
              class="img"
              alt=""
              id="home-landing-img"
          />
        </div>
        <div class="left-bottom">
          <h2>Join Us</h2>
          <p>We're building a Community for Creatives and Creators. And we'll like you to be a part of this new budding community of talented individuals.</p>
          <div class="form">
            <h2 class="header">Subscribe</h2>
             <b-form v-on:submit="onSubmit" v-on:reset="onReset" v-if="show">
              <b-form-group
                id="input-group-1"
                label-for="input-1"
              >
                <b-form-input
                  id="input-1"
                  v-model="form.email"
                  type="email"
                  placeholder="Email Address"
                  required
                >
                </b-form-input>
              </b-form-group>

              <b-form-group 
                id="input-group-2" 
                label-for="input-2"
              >
                <b-form-input
                  id="input-2"
                  v-model="form.name"
                  placeholder="Name"
                  required
                ></b-form-input>
              </b-form-group>              
              <b-button type="submit" variant="primary">Join Our Waitlist</b-button>
              <!-- <b-button type="reset" variant="danger">Reset</b-button> -->
            </b-form>   
            <div class="form-footer">
              We respect your privacy, Unsubsribe at anytime.
            </div>         
          </div>
        </div>
      </div>     
       <div class="right">        
        <img
            src="assets/images/join.jpg"
            class="img"
            alt=""
            id="home-landing-img"
        />
      </div> 
    </div>
  </div>
</template>

<script>
import {
  ValidationProvider, 
  ValidationObserver
  } from 'vee-validate';
import {local_url, endPoints} from '../utils/http'
import axios from 'axios'

export default {
  name: 'IndexPage',

  components: {
    ValidationProvider,
    ValidationObserver
  },

  data () {
    return {
      image: '',
      form: {
          email: '',
          name: '',         
      },
      isLoading: false,
      foods: [{ text: 'Select One', value: null }, 'Carrots', 'Beans', 'Tomatoes', 'Corn'],
      show: true,
      url: '',
    }
  },
  methods: {
    onSubmit(event) {
      event.preventDefault()
      this.isLoading = true
      //alert(JSON.stringify(this.form))
      console.log(this.form)   
      this.url = local_url  
      console.log(this.url)
      this.getPost()
    },
    onReset(event) {
      event.preventDefault()
      // Reset our form values
      this.form.email = ''
      this.form.name = ''      
      // Trick to reset/clear native browser form validation state
      this.show = false
      this.isLoading = false
      this.$nextTick(() => {
      this.show = true
      })
    },

    getPost(){
        axios.get(`${local_url}/${endPoints.test}`).then((response) => {
            console.log(response.data);
        });
    }
    // async function getPost(){
    //       const response = await client.get('/1');
    //       setPosts(response.data);
    // }

  }
}
</script>

<style lang="scss">
@import '../static/scss/_config';

.wait-list{
  width: var(--full);
  height: 100%;
  background-color: var(--background-color);
  display: flex;
  align-items: center;
  justify-content: center;

  &-col{
    background-color: #fff;
    width: 60%;
    height: 80%;
    border-radius: 10px;
    display: flex;
    margin: 30px 0;

    // @media (max-width: 1024px) {
    //   flex-direction: row-reverse;
    // }

    @media (max-width: 480px) {
      flex-direction: column-reverse;
      width: 95%;      
    }

      .left{
        background-color: var(--white);
        height: 100%;
        width: 50%;
        border-top-left-radius: 10px;
        border-bottom-left-radius: 10px;
        display: flex;
        flex-direction: column;

        @media (max-width: 480px) {
          display: flex;
          width: 100%;
          border-bottom-right-radius: 10px;
        }

          &-top{
            img{
              width: 100%;
              height: 200px;
              border-top-left-radius: 10px;
            }            
          }

          &-bottom{
            width: 100%;
            margin: 10px 0;
            padding: 0 20px;

            @media (max-width: 480px) {
              padding: 0 17px;
            }

            .form{
              width: 100%;    
              
              b-form{
                width: inherit;

                b-form-group{
                  input{
                    background-color: #d9d9d9;
                    border-radius: 0;
                  }
                }
                
              }

              .form-group{

                input{
                  background-color: #d9d9d9;
                  height: 50px;
                  border-radius: 0;
                }
              }
              .btn{
                background-color: #0f2b53;
                color:  var(--white);
                width: 100%;
                height: 50px;
                border-radius: 0;
              }

              .form-footer{
                font-size: 12px;
                text-align: center;
                color: #bbb8b8;
                margin-top: 20px;
              }
            }
          }
      }

     

      .right{
        background-color: brown;
        height: 100%;
        width: 50%;
        border-top-right-radius: 10px;
        border-bottom-right-radius: 10px;

        @media (max-width: 480px) {
          width: 100%;
        }

        .img{
          height: 100%;
          width: 100%;
          border-top-right-radius: 10px;

          @media (min-width: 481px) {
            border-bottom-right-radius: 10px;
          }

          @media (max-width: 480px) {
            border-top-right-radius: 10px;
            border-top-left-radius: 10px;
            height: 200px;
          }
        }
      }
  }

  .loginBut{
    padding: 7px 25px !important;
    letter-spacing: 0px;
    font-weight: 600;
    margin-top: 25px;
    border-radius: var(--border-radius);
    width: 125px;
    background: var(--blue) !important;
    color: var(--white);
  }
}
</style>
