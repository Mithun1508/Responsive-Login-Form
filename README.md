# Build a responsive login form using HTML and SCSS.

Here we have created a main container div and the whole form is divided in two main sections.

Section one will contain the social links and the main form. While Section two only has a button.

HTML BOILERPLATE 

<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta http-equiv="X-UA-Compatible" content="IE=edge" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <link rel="stylesheet" href="index.css" />
    <title>Login Signup Form</title>
  </head>
  <body>
    <div class="container">
      <div class="section-one">
        <div class="social-links">
          <div class="facebook">
            <span> LOGIN WITH FACEBOOk </span>
            <div class="icon">
              <img src="./assets/facebookLogo.svg" alt="" />
            </div>
          </div>
          <div class="twitter">
            <div class="icon">
              <img src="./assets/twitterLogo.svg" alt="" srcset="" />
            </div>
            <span> LOGIN WITH TWITTER </span>
          </div>
        </div>
        <div class="main-form">
          <input type="email" name="email" placeholder="Email" />
          <input type="password" name="password" placeholder="Password" />
          <a href="#">I forgot my password?</a>
          <button>Login</button>
        </div>
      </div>

      <div class="section-two">
        <div class="new-account">
          <button>Create New Account</button>
        </div>
      </div>
    </div>
  </body>
</html>
# used SCSS to code this form.

These are the color variables which will be used throughout the form.
$gradientColor1: #560bad;
$gradeintColor2: #8e60c4;
$formBackgroundColor: #300169;
$pinkOutline: #a31a6a;
$loginButtonColor: rgb(96, 196, 96);
$loginButtonTextColor: white;
$newAccountButtonColor: #ffd60a;
$newAccountButtonTextColor: rgb(36, 34, 34);
$inputBackgroundColor: #2b045c;
$inputPlaceholderColor: rgba(255, 255, 255, 0.548);
$loginWithAccountsTextColor: white;
$inputTextColor: white;
$forgetHoverColor: white;

# Mixins

We Will be using mixins in the login form. Mixins works as a normal function in any language.

Mixin #1
# flexbox properties. 

We will be using the flexbox properties in many places so it's better to create a mixin for that.
@mixin enableFlex($direction: false) {
  display: flex;
  align-items: center;
  justify-content: center;
  @if $direction {
    flex-direction: column;
  }
}

#Here we have also used an optional parameter for the flexbox direction. We have used @if rule to check if the parameter is true. If you don't pass any parameters while including the mixin then it will take false by default.

# including the mixin by @include enableFlex();

Mixin #2
Our second mixin would be for the button elements.
@mixin buttonStyles($backgroundColor, $fontColor) {
  padding: 0.8rem 1.5rem;
  width: 22rem;
  border-radius: 0.2rem;
  outline: none;
  border: none;
  font-size: medium;
  background-color: $backgroundColor;
  color: $fontColor;
  cursor: pointer;
  transition: background 0.5s;
  &:hover {
    background: darken($backgroundColor, 20%)
      radial-gradient(circle, transparent 1%, darken($backgroundColor, 20%) 1%)
      center/15000%;
  }
  &:active {
    background-color: darken($backgroundColor, 30%);
    background-size: 100%;
    transition: background 0s;
  }
}
 passed bG color and the text color to the mixin.

Now we will apply some global styling to the page.
* {
  font-family: $mainFont;
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}
body {
  background: linear-gradient(to right, $gradientColor1, $gradeintColor2);
  height: 100vh;
  width: 100vw;
  @include enableFlex();
}
Now we will apply some styles to our input elements.
input {
  padding: 0.8rem 1rem;
  width: 22rem;
  border-radius: 0.2rem;
  border: $pinkOutline 0.01rem solid;
  color: $inputTextColor;
  background-color: $inputBackgroundColor;
  margin-bottom: 0.8rem;
  font-size: large;
  &::placeholder {
    color: $inputPlaceholderColor;
  }
}
Now the below code would be for our main form.

.container {
  height: 75vh;
  width: 80vw;
  background-color: $formBackgroundColor;
  .section-one {
    @include enableFlex(true);
    height: 80%;
    border-bottom: 0.05rem $pinkOutline solid;
    .social-links {
      display: flex;
      margin-bottom: 2rem;
      position: relative;
      height: 20%;
      cursor: pointer;
      .facebook {
        @include enableFlex();
        position: absolute;
        left: -10.5rem;
        span {
          width: 52%;
          color: $loginWithAccountsTextColor;
          font-size: 0.8rem;
          padding-right: 0.4rem;
        }
        .icon {
          height: 6rem;
          width: 6.5rem;
          border-radius: 100%;
          border: $pinkOutline 0.1rem solid;
          @include enableFlex();
          cursor: pointer;
          img {
            height: 4rem;
          }
        }
      }
      .twitter {
        @include enableFlex();
        position: absolute;
        right: -12rem;
        span {
          width: 50%;
          color: $loginWithAccountsTextColor;
          padding-left: 0.4rem;
          font-size: 0.8rem;
        }
        .icon {
          height: 6rem;
          width: 6.3rem;
          border-radius: 100%;
          border: $pinkOutline 0.1rem solid;
          @include enableFlex();
          background-color: $formBackgroundColor;
          box-shadow: -0.5rem 0px $formBackgroundColor;

          img {
            height: 4rem;
          }
        }
      }
    }
    .main-form {
      @include enableFlex(true);
      button {
        @include buttonStyles($loginButtonColor, $loginButtonTextColor);
      }
      a {
        text-decoration: none;
        @include enableFlex();
        color: $pinkOutline;
        font-weight: bold;
        margin-bottom: 2rem;
        transition: 0.3s ease-in-out;
        &:hover {
          color: $forgetHoverColor;
        }
      }
    }
  }
  .section-two {
    height: 20%;
    @include enableFlex();
    button {
      @include buttonStyles($newAccountButtonColor, $newAccountButtonTextColor);
    }
  }
}


# used some Media Queries for adding responsiveness.

@media only screen and (max-width: 768px) {
  .container {
    height: 35rem;
    .section-one {
      .social-links {
        .facebook {
          left: -8.2rem;
          span {
            font-size: small;
            padding-right: 0.9rem;
          }
          .icon {
            height: 4rem;
            width: 4rem;
            border-radius: 100%;
            img {
              height: 3rem;
            }
          }
        }
        .twitter {
          right: -10rem;
          span {
            font-size: small;
          }
          .icon {
            height: 4rem;
            width: 4rem;
            border-radius: 100%;
            img {
              height: 3rem;
            }
          }
        }
      }
      .main-form {
        input {
          width: 15rem;
        }
        button {
          width: 15rem;
        }
      }
    }
    .section-two {
      button {
        width: 15rem;
      }
    }
  }
}
That's it !! Do check it out below link.

# site is Live Now: https://csb-uuysxh.netlify.app/
