<template>
  <div id="app" class="app">
    <div class="grid-x">
      <section id="form-section" class="form-section">
        <h1>hCard Builder</h1>
        <form id="main-form" action="#" method="" enctype="text/plain" title="Please fill the form below ">
          <fieldset>
            <legend>Personal Details</legend>
            <div class="row">              
              <div class="cell">
                <label for="given-name">Given Name</label>
                <input type="text" id="given-name" class="input" name="given-name" placeholder="Sam" v-model="userData.givenName" required />
              </div>    
              <div class="cell">
                <label for="surname">Surname</label>
                <input type="text" id="surname" class="input" name="surname" placeholder="Fairfax" v-model="userData.surname" required/>
              </div>              
            </div>
            <div class="row">
              <div class="cell">
                <label for="email">Email </label>
                <input type="email" id="email" class="input" name="email" placeholder="sam.fairfax@fairfaxmedia.com" v-model="userData.email" required />
              </div>
              <div class="cell">
                <label for="phone">Phone</label>
                <input type="tel" id="phone" class="input" name="phone" placeholder="02 9282 2833" pattern="[0-9]{2}-[0-9]{4}-[0-9]{4}" v-model="userData.phone"  required />
              </div> 
            </div>
          </fieldset>                  
          <fieldset>
            <legend>Address</legend>
            <div class="row">
              <div class="cell">
                <label for="house-name-or-number">House Name or #</label>
                <input type="text"  id="house-name-or-number" class="input" name="houseDetail" placeholder="1" v-model="userData.houseDetail"/>
              </div>
              <div class="cell">
                <label for="street">Street</label>
                <input type="text" id="street" class="input" name="street" placeholder="Darling Island Road" v-model="userData.street"/>
              </div>
            </div>
            <div class="row">
              <div class="cell">
                <label for="suburb">Suburb</label>
                <input type="text" id="suburb" class="input" name="suburb" placeholder="Pyrmont" v-model="userData.suburb"/>
              </div>
              <div class="cell">
                <label for="state">State</label>
                <input type="text" id="state" class="input" name="state" placeholder="NSW" v-model="userData.state"/>
              </div>
            </div>
            <div class="row">
              <div class="cell">
                <label for="postcode">Postcode</label>
                <input type="text" id="postcode" class="input" name="postcode" placeholder="2009" v-model="userData.postcode"/>
              </div>
              <div class="cell">
                <label for="country">Country</label>
                <input type="text" id="country" class="input" name="country" placeholder="Australia" v-model="userData.country"/>
              </div>
            </div>
            <div class="row button-section">
              <div class="cell">               
                <label for="files" class="button upload">Upload Avatar</label>
                <input type="file" v-on:change="uploadAvatar" id="files" name="avatar-input" class="show-for-sr" accept=".jpg,.jpeg.,.png" />     
              </div>
              <div class="cell"> 
                  <input type="submit" id="button-submit" value="Create hCard" class="button create" title="Submit the form" />
              </div>              
            </div>
          </fieldset>      
         
        </form>
      </section>
      <section id="preview-section" class="preview-section">
        <h2>Hcard Preview</h2>
        <div class="hcard">          
          <h3>
            <label id="given-name-preview"> {{userData.givenName}} </label> 
            <label id="surname-preview"> {{userData.surname}} </label>
            <img v-bind:src="image" id="preview-img" alt="Preview your avatar" title="preview your avatar" v-on:click="uploadAvatar">
          </h3>          
          <p>
            <label>Email </label> 
            <span class="email"> {{userData.email}} </span>
          </p>
          <p>
            <label>Phone </label> 
            <span id="phone-preview"> {{userData.phone}} </span>
          </p>
          <p>
            <label>Address</label>
            <span id="house-name-or-number"> {{userData.houseDetail}} </span>
            <span id="street-preview"> {{userData.street}} </span>
          </p>
          <p>
            <label></label>
            <span id="suburb-preview"> {{userData.suburb}} </span>
            <span id="state-preview"> {{userData.state}} </span>
          </p>
          <p>
            <section>
              <label>Postcode</label>
              <span id="postcode-preview"> {{userData.postcode}} </span>
            </section>
            <section>
              <label>Country</label>
              <span id="country-preview"> {{userData.country}} </span>
            </section>
          </p>          
        </div> 
      </section>
    </div>
  </div>
</template>

<script>
export default {
  name: 'app',
  data () {
    return {
      userData: {
        givenName:'',
        surname:'',
        email:'',
        phone:'',       
        houseDetail:'',
        suburb:'',
        street:'',
        state:'', 
        postcode:'',
        country:''
      },
      image:'./img/preview.png'
    }
  },
  methods:{   
    uploadAvatar(e) {
      var files = e.target.files || e.dataTransfer.files;
      if (!files.length)
        return;
      this.createImage(files[0]);
    },
    createImage(file) {
      var image = new Image();
      var reader = new FileReader();
      var vm = this;

      reader.onload = (e) => {
        vm.image = e.target.result;
      };
      reader.readAsDataURL(file);
    }    
  }
}
</script>

<style lang="scss">

/**
 * Global Config
 */

//Background Colors
$body-bgcolor:            grey;
$button-color:            #fff;
$button-create-bgcolor:   #3fa9e2;
$button-upload-bgcolor:   #758E9D;
$form-section-bgcolor:    #fff;
$hcard-bgcolor:           #fff;
$preview-section-bgcolor: #e7e9ec;

//Colors
$heading1-color:          #394F63;
$heading3-color:          #fff;
$heading3-bgcolor:        #394f63;
$label-color:             #2c3e50;
$legend-color:            #b0b8bc; 
$placeholder-color:       #6d7578;
$separator-color:         #dbe0e2;
$text-box-color:          #dbe0e2;

//Font Stacks
$font-url--primary:      'https://fonts.googleapis.com/css?family=Merriweather+Sans:400,700,800';
$font-url--secondary:    'https://fonts.googleapis.com/css?family=Merriweather:400,700,900';

//Font Families
$font-family--primary:   'Merriweather Sans', sans-serif;
$font-family--secondary: 'Merriweather', serif;

//Font Styles
$font-style--normal:      normal;

//Font Weights
$font-weight--light:      300;
$font-weight--medium:     400;
$font-weight--bold:       700;
$font-weight--ultra-bold: 800;

//Media Queries
@mixin mq($break) {
  // Small only
  @if $break == "small" {
    @media screen and (max-width: 39.9375em) {
      @content;
    }
  }
  // Medium and up
  @else if $break == "medium" {
    @media screen and (min-width: 40em) {
      @content;
    }
  }
  // Large and up
  @else if $break == "large" {
    @media screen and (min-width: 64em) {
      @content;
    }
  }
  @else {
    @error "Whoops! No value could be retrieved for #{$break}."
  }
}

//Utilities

//import if google fonts url is defined

@if variable-exists(font-url--primary){
  @import url($font-url--primary)
}
@if variable-exists(font-url--secondary){
  @import url($font-url--secondary)
}

//Base
*, *:before, *:after {
  -moz-box-sizing: border-box;
  box-sizing: border-box;
  margin:0;
  padding:0;
}

/**
 * Application
 */

//the main wrapper

.app {

  @include mq(large) {
    width:1000px;
    margin-top:5rem;
  }  

  .grid-x {
    @include mq(large) {
      display: flex;    
      flex-wrap:wrap;
      padding-top:3rem;
    }

    & >section {
      @include mq(large) {       
        width: 50%;
      }
    }
  }
}

body {
  background: $body-bgcolor;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;  

  @include mq(large) {
    display: flex;    
    flex-wrap: wrap;    
    justify-content: center;
    min-height: 100vh;
  }  
}

//button

.button {
  border: 0;
  border-radius: 4px;
  color: $button-color;
  cursor: pointer;
  font-family: $font-family--primary;
  font-size: 1.25em;
  font-weight: $font-weight--light;
  outline: none;  
  margin: 0 0 .5em;  
  padding: .5em 0.5em;
  text-align: center;
  white-space: nowrap;
  width: 100%;  

  &.create {
    background: $button-create-bgcolor;
    border-bottom: 3px solid darken($button-create-bgcolor,10%);
  }

  &.upload {
    background: $button-upload-bgcolor;
    border-bottom: 3px solid darken($button-upload-bgcolor,10%);
    text-transform: capitalize;
  }
}

.button-section {
  margin: 0.85rem 0 1.5em;
}

//Form 

form {  

  .input {
    background-color: #fefefe; 
    border: 1px solid $text-box-color;
    border-radius: 4px;
    display: block;    
    font-family: $font-family--secondary;
    font-size: 1.1rem;
    font-weight: $font-weight--medium;   
    height: 2.2rem;
    margin: 0 0 1rem;
    outline: 0;
    padding: .25rem .5rem;    
    text-overflow: ellipsis;
    width: 100%;

    &::placeholder {
      color: $placeholder-color;
    }
  }  
}

fieldset {
  border: 0;
  margin: 0;
  padding: 0;
  text-transform:uppercase;

  .cell {

    @include mq(medium) {
      width:50%;
      padding-right: .5rem;
      padding-left: .5rem;
    }
  }

  input[type="file"] {
    display:none;
  }

  label {
    display: block;
    font-size: 0.78rem;
    font-family: $font-family--primary;
    font-weight: $font-weight--medium;
    padding:0 0.2rem;
    text-transform: uppercase;    
  }

  legend {
    border-bottom: 1px solid $separator-color;
    color: $legend-color;
    font-family: $font-family--primary;
    font-weight: $font-weight--medium;
    font-size: .75rem;
    margin: 0 0 1.5rem;
    padding: 1rem 0 .16rem;
    width: 100%;
  }

  .row {
    @include mq(medium) {
      display: flex;
      margin-right: -.5rem;
      margin-left: -.5rem;
    }    
  }  
}

.form-section {
  background: $form-section-bgcolor; 
  padding: 0 1rem;

  @include mq(medium) {
    padding: 0 6rem;
  }

  @include mq(large) {
    padding: 0 2.2rem;
  }
}

//Headings

h1,h2 {  
  font-family: $font-family--primary; 
  font-weight: $font-weight--bold;
}

h1 {
  color: $heading1-color;
  font-size: 1.7rem;  
  margin:0 0 0.5rem;
  padding: 2rem 0 0; 
}

h2 {
  color: $legend-color;  
  font-size: 0.95rem;
  margin: 0;
  padding: 0 0 .5rem;  
  text-align: right;
  text-transform: uppercase;
}

h3 {
  background:$heading3-bgcolor;
  color: $heading3-color;
  font-family: $font-family--secondary;
  font-size: 1.8rem;  
  font-weight: $font-weight--medium; 
  height: 5.5rem;
  margin: 0 0 1rem;
  padding: 2.2rem 1rem 1.2rem;
  position: relative;
  text-transform: capitalize;

  img {
    font-size: 1rem;
    height: 105px;
    position: absolute;  
    right: .5rem;
    top: .5rem;
    width: 82px;
  }
}

//hCard or Preview Section

.hcard {
  background: $hcard-bgcolor;
  padding: 0 0 1rem;

  p {
    border-bottom: 1px solid $separator-color;
    display: block;
    margin: 0 1.5rem .5rem;  

    label {
      display: inline-block;
      font-family: $font-family--primary;
      font-size: .7rem;
      text-transform: uppercase;
      width: 70px;
    }

     &:last-child {
       display: flex;

       section {
          flex: 1;
       }
    }

    span {
      font-family: $font-family--secondary;
      font-size: 1.1rem;
      text-transform: capitalize;

      &.email {
        text-transform: lowercase;
      }
    }    
  }
}

.preview-section {
  background-color: $preview-section-bgcolor;
  margin: 0;
  padding: 3rem 1rem;

  @include mq(medium) {
    padding: 3rem 6rem;
  }

  @include mq(large) {
    padding: 5rem 2.5rem;
  }
}

.show-for-sr {
  border: 0;
  clip: rect(0,0,0,0);
  height: 1px;
  overflow: hidden;
  padding: 0;
  position: absolute!important;
  -webkit-clip-path: inset(50%);
  clip-path: inset(50%);
  white-space: nowrap;
  width: 1px;
}

</style>
