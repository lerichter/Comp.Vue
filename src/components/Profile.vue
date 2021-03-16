<template>
  <div>
    <div class="row">
      <div class="col-md-4">
        <div class="card" style="width: 20rem;">
          <img class="card-img-top" :src="user.avatar_url"/>
          <ul class="list-group list-group-flush"> 
            <li class="list-group-item">Repositories: <span class="badge badge-success">{{ user.public_repos }}</span></li>
            <li class="list-group-item">Followers: <span class="badge badge-primary">{{ user.followers }}</span></li>
            <li class="list-group-item">Following: <span class="badge badge-info">{{ user.following }}</span></li>          
          </ul>
          <div class="card-body">
            <a :href="user.html_url" class="btn btn-warning btn-block">See Profile</a>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>
<script>
export default {
  props: ["user"]
}
</script>