<template>
  <div>
    <div class="d-flex topnav" style="margin-top: 44px">
      <div>
        <img class="headerlogo" src="~/assets/img/logo.png" />
      </div>
      <div class="ml-auto">
        <button class="navbar-toggler" type="button" hidden>
          <span class="navbar-toggler-icon"></span>
        </button>

        <div class="">
          <ul class="navbar-nav ml-auto" style="">
            <li class="nav-item">
              <a class="nav-link" href="https://wewannalearn.com/#aboutus">有關我們 </a>
            </li>
            <li class="nav-item">
              <a class="nav-link" href="https://wewannalearn.com/#tutor">導師介紹</a>
            </li>
            <li class="nav-item">
              <a class="nav-link" href="https://wewannalearn.com/teach">導師招募</a>
            </li>

            <li class="nav-item" style="background: #007bff; color: white; border-radius: 10px">
              <a class="nav-link" href="https://app.wewannalearn.com">登入平台</a>
            </li>
          </ul>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  setup() {},
  mounted: function () {},
}
</script>
>

<style scoped>
.navlist {
  display: none;
}

.logoutbutton {
  background: white;
  color: var(--wewannalearn-orange);
  font-size: 12px;
  text-align: center;
  vertical-align: middle;
  padding-top: 5px;
  padding-bottom: 5px;
  font-weight: 900;
  width: 60px;
  margin-right: 62px;
  margin-top: 10px;
  border: 0px solid white;
  border-radius: 20px;
  z-index: 1;
}

.logoutbutton:hover {
  cursor: pointer;
}

.headerlogo {
  margin-left: 83px;
  width: 150px;
}

.topnav {
  z-index: 999;
  position: relative;
}

.menubutton {
  display: none;
}

@media screen and (max-width: 991px) {
  .headerlogo {
    margin-left: 30px;
    width: 150px;
  }

  .navlist {
    width: 100%;
    display: block;
    margin-top: 50px;
    margin-bottom: -30px;
  }

  .navlist > div > div {
    border-bottom: 2px solid #eee;
    padding-bottom: 4px;
  }

  .navunfocus:hover {
    cursor: pointer;
  }

  .navunfocus {
    opacity: 0.5;
    border-bottom: none !important;
  }

  .logoutbutton {
    /* display: none; */
    margin-right: 30px;
  }

  .menubutton {
    display: block;

    margin-right: 30px;
    font-size: 30px;
  }
}

.nav-link {
  color: rgba(255, 255, 255, 0.7);
  padding-right: 0.5rem;
  padding-left: 0.5rem;
  display: block;
  padding: 0.5rem 1rem;
}

.navbar-nav {
  flex-basis: auto;
  -webkit-box-flex: 1;
  -ms-flex-positive: 1;
  flex-grow: 1;
  align-items: center;
  display: -webkit-box;
  display: -ms-flexbox;
  display: flex;
  -webkit-box-orient: vertical;
  -webkit-box-direction: normal;
  -ms-flex-direction: column;
  flex-direction: column;
  padding-left: 0;
  margin-bottom: 0;
  list-style: none;
  /* display: block; */
  padding: 0.5rem 1rem;
  -webkit-box-orient: horizontal;
  -webkit-box-direction: normal;
  -ms-flex-direction: row;
  flex-direction: row;
}

.navbar-toggler-icon {
  background-image: url("data:image/svg+xml;charset=utf8,%3Csvg viewBox='0 0 30 30' xmlns='http://www.w3.org/2000/svg'%3E%3Cpath stroke='rgba(255, 255, 255, 0.5)' stroke-width='2' stroke-linecap='round' stroke-miterlimit='10' d='M4 7h22M4 15h22M4 23h22'/%3E%3C/svg%3E");
  color: rgba(255, 255, 255, 0.5);
  border-color: rgba(255, 255, 255, 0.1);
}
</style>
