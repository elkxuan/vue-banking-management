<template>
  <nav class="navbar navbar-expand-sm bg-dark navbar-dark">
    <div class="container-fluid">
      <a class="navbar-brand" href="#">Banking Management System</a>
      <button class="navbar-toggler" type="button" data-bs-toggle="collapse" data-bs-target="#collapsibleNavbar">
        <span class="navbar-toggler-icon"></span>
      </button>
      <div class="collapse navbar-collapse" id="collapsibleNavbar">
        <ul class="navbar-nav">
          <li class="nav-item">
            <router-link class="nav-link" to="/">Home</router-link>
          </li>
          <li class="nav-item">
            <router-link class="nav-link" to="/department">Department</router-link>
          </li>
          <li class="nav-item">
            <router-link class="nav-link" to="/employee">Employee</router-link>
          </li>
          <li class="nav-item">
            <router-link class="nav-link" to="/customer">Customer</router-link>
          </li>
          <li class="nav-item dropdown">
            <a class="nav-link dropdown-toggle" href="#" role="button" data-bs-toggle="dropdown">Account</a>
            <ul class="dropdown-menu">
              <li><router-link class="dropdown-item" to="/account">Account</router-link></li>
              <li><router-link class="dropdown-item" to="/transaction">Transaction</router-link></li>
            </ul>
          </li>
        </ul>
        <ul class="navbar-nav" style="margin-left: auto;">
          <li class="nav-item">
            <a class="nav-link" href="#">Logout</a>
          </li>
        </ul>
      </div>
    </div>
  </nav>

  <div class="container-fluid mt-3">
    <router-view />
  </div>
</template>
