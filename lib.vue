function movieSelected(id) {
  sessionStorage.setItem('cidadeId', id);
  window.location = 'cidade.html';
  return false;
}

function getMovie() {
  let cidadeId = sessionStorage.getItem('cidadeId');
  
  
  axios.get('https://api.openweathermap.org/data/2.5/weather?q='+cidadeId+'&appid=375b5b72defecfdfccfa090d50f49db4')
        .then((response) => {
          console.log(response);
          let cidade = response.data;
      
      let output = `
        <div class="row">
          <div class="col-md-4">
          <img src="weather-icon-1.ico" >
          </div>
          <div class="col-md-8">
            <h2>${cidade.name}</h2> 
            <ul class="list-group">
              <li class="list-group-item"><b>Temp: </b>${cidade.main.temp}</li>
              <li class="list-group-item"><b>Feel: </b>${cidade.main.feels_like}</li>
              <li class="list-group-item"><b>Pressao: </b>${cidade.main.pressure}</li>
              <li class="list-group-item"><b>Humidade: </b>${cidade.main.humidity}</li>
              <li class="list-group-item"><b>Temp.max: </b>${cidade.main.temp_min}</li>
              <li class="list-group-item"><b>Temp.max: </b>${cidade.main.temp_max}</li>
            </ul>
          </div>
        </div>
        <div class="row">
          <div class="well">
            
           
            <a href="index.html" class="btn btn-secondary">Voltar</a>
          </div>
        </div>
      `;
      
      this.detalhes=  $('#cidade').html(output);
    })
    .catch((err) => {
      console.log(err);
    });      
 }  




 Vue.createApp({

    data() {
    return {
      cidade: null,
      detalhes:null,
      guardar:''
    }
  },
  created() {
  
    setTimeout(() => this.list(), 500);
    },
    methods:{
   
        list:function(){
      const cds = ['Maputo',"Nairobi", "Luanda", "Cairo", "Dakar", "Lisboa", "Madrid", "Paris"];
      let output = '';
       $.each(cds, (index, cida) => {
     
      //for (let i = 0; i < cds.length; i++) {
       //alert(cds[i])
        axios.get('https://api.openweathermap.org/data/2.5/weather?q='+cida+'&appid=375b5b72defecfdfccfa090d50f49db4')
        .then((response) => {
          console.log(response);
          let cidade = response.data;
         
          
            output+= `
              <div class="col-md-6">
                <div class="p-5 text-center">
                <h5 class="text-dark">${cida}</h5>
                <img src="weather-icon-1.ico" >
                  <h5>Máxima: (${cidade.main.temp_max})</h5>
                  <h5>Mínima: (${cidade.main.temp_min})</h5>
                  <a onclick="movieSelected('${cida}')" class="btn btn-primary mb-3" href="cidade.html">Ver mais</a>
                  
                </div>
              </div>
            `;
            this.cidade=$('#cidades').html(output);
           });
         
          //alert(cidade.main.temp)
        })
       
      
      //}
       
     

     
        },

        movieSelected:function(id) {
          alert('dd')
          sessionStorage.setItem('movieId', id);
          window.location = 'cidade.html';
          return false;
        },
        getMovie:function() {
          let movieId = sessionStorage.getItem('movieId');
          
          
          axios.get('http://www.omdbapi.com?i='+tt1228705+'&apikey=6149a617')
            .then((response) => {
              console.log(response);
              let cidade = response.data;
              
              let output = `
                <div class="row">
                  <div class="col-md-4">
                    <img src="${cidade.Poster}" class="thumbnail">
                  </div>
                  <div class="col-md-8">
                    <h2>${cidade.Title}</h2> 
                    <ul class="list-group">
                      <li class="list-group-item"><b>Genre: </b>${cidade.Genre}</li>
                      <li class="list-group-item"><b>Released: </b>${cidade.Released}</li>
                      <li class="list-group-item"><b>Rated: </b>${cidade.Rated}</li>
                      <li class="list-group-item"><b>IMDB Rating: </b>${cidade.imdbRating}</li>
                      <li class="list-group-item"><b>Director: </b>${cidade.Director}</li>
                      <li class="list-group-item"><b>Actors: </b>${cidade.Actors}</li>
                    </ul>
                  </div>
                </div>
                <div class="row">
                  <div class="well">
                    <h3>Plot</h3>
                    ${cidade.Plot}
                    <hr>
                    <a href="http://imdb.com/title/${cidade.imdbID}" target="_blank" class="btn btn-primary">View IMDB</a>
                    <a href="index.html" class="btn btn-light">Go Back to Search</a>
                  </div>
                </div>
              `;
              
              this.detalhes=$('#cidade').html(output);
            })
            .catch((err) => {
              console.log(err);
            });      
         }  

        
       

        
    }
  }).mount('#c')



  

