

<template>
  <div class="container-fluid">
    <div class="row">
      <div v-for="member in members" v-bind:key="member.id" class="card col-sm-12 col-md-6 col-lg-3" style="margin: 1em">
        <img v-if="member.gender == 'F'" src="../public/kepek/female.png" class="card-img-top" alt="Szépséges tagunk képe">
        <img v-if="member.gender == 'M'" src="../public/kepek/male.png" class="card-img-top" alt="Szépséges tagunk képe">
        <img v-if="member.gender == null" src="../public/kepek/female.png" class="card-img-top" alt="Szépséges tagunk képe">
        <div class="card-body">
          <h4 class="card-title">{{member.name}}</h4>
          <p class="card-text">Születésnap: {{member.birth_date}}</p>
          <p class="card-text">Csatlakozási idő: {{member.created_at}}</p>
        </div>
      </div>
    </div>

  <div class="form-group">
    <label for="nev">Név</label>
    <input type="text" class="form-control" id="nev" placeholder="Enter name">
  </div>
  <div class="form-group">
    <label for="szul_datum">Születési dátum</label>
    <input type="datetime-local" class="form-control" id="szul_datum" placeholder="Birth date">
  </div>
  <div class="form-group">
    <label for="nem">Nem</label>
    <select name="nem" id="nem" class="form-control">
      <option value="F">Nő</option>
      <option value="M">Férfi</option>
    </select>
  </div>
  <button type="submit" class="btn btn-primary">Submit</button>
</div>
</template>

<script>
export default {
  name: 'App',
  data() {
    return {
      member: {
        id: null,
        name: null,
        gender: null,
        birth_date: null,
        banned: null,
        created_at: null
      },
      members: []
    }
  },
  methods: {
    async loadMembers() {
      let response = await fetch('http://127.0.0.1:8000/api/members')
      let data = await response.json()
      this.members = data
      console.log(this.members)
    }
  },
  mounted() {
    this.loadMembers()
  },
}
</script>
