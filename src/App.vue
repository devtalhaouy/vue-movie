<template>
<div class="container">
  <header>
  <router-link to="/">
  <h1>Movie<span>Vue</span></h1>
  </router-link>
</header>
  <main>
    <router-view/>
  </main>
  <footer>
    <h4>created by <a href="mailto:talhaouy.dev@gmail.com">Mhammed Talhaouy</a></h4>
  </footer>
</div>
</template>

<style lang="scss">
*{
  margin: 0;
  padding: 0;
  box-sizing: border-box;
  font-family: 'Fira Sans',sans-serif;
  &::selection{
    background: transparentize(#42b883,0.5);
  }
}
body{
 background: #355C7D;  /* fallback for old browsers */
background: -webkit-linear-gradient(to right, #C06C84, #6C5B7B, #355C7D);  /* Chrome 10-25, Safari 5.1-6 */
background: linear-gradient(to right, #C06C84, #6C5B7B, #355C7D); /* W3C, IE 10+/ Edge, Firefox 16+, Chrome 26+, Opera 12+, Safari 7+ */


}
a{
  text-decoration: none;
}
header{
  display: flex;
  align-items: center;
  justify-content: center;
  padding: 10px 16px;
  background-color: #2c3d4e;
  box-shadow: 0px 0px 6px rgba(0,0,0,0.1);
  h1{
    color: #fff;
    font-size: 28px;
    span{
      color:#42b883;
    }
  }
}
footer{
  background: #2c3d4e;
  padding: 5px 0;
  h4{
    text-align:center;
    color:#fff;
    text-transform: capitalize;
    a{
      color:#355C7D;
      font-weight: 400;
      transition: .5s ease;
      &:hover{
        color:#6792b8;
        cursor: pointer;
      }
    }
  }
}
</style>