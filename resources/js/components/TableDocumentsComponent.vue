<template>
    <div class="container">
        <div class="row justify-content-center">
            <div class="col-md-10">
                <div class="card">
                    <div class="card-header"><h2>Listado de Documentos</h2></div>

                    <div class="card-body">
                      <table class="table" id="table_documents">
                        <thead>
                          <tr>
                            <th scope="col">Nombre</th>
                            <th scope="col">Descripción</th>
                            <th scope="col">Archivo</th>
                            <th scope="col">Fecha de vencimiento</th>
                            <th scope="col">Fecha de notificación</th>
                            <th scope="col">Cliente</th>
                            <th scope="col">Opciones</th>
                          </tr>
                        </thead>
                        <tbody>
                          <tr v-for="document in documents">
                            <td>{{ document.name }}</td>
                            <td>{{ document.description }}</td>
                            <td>{{ document.file }}</td>
                            <td>{{ document.expiration_date }}</td>
                            <td>{{ document.reminder_date }}</td>
                            <td>{{ document.client.name }}</td>
                            <td></td>
                          </tr>
                          </tr>
                        </tbody>
                      </table>
                    </div>
                </div>
            </div>
        </div>

        

        
    </div>
</template>

<script>
    import datatables from 'datatables'
    export default {
        mounted(){
            this.getDocuments();
        },
        data: function() { 
            return {
                documents: [],
                client_fisico: {
                    id: '',
                    name: '',
                    phone: '',
                    email: '',
                    rfc: '',
                    curp: '',
                    address:''
                },
                client_moral: {
                    id: '',
                    name: '',
                    phone: '',
                    email: '',
                    rfc: '',
                    business_name: '',
                    address:'',
                    turn: ''
                }
            }
        },
        methods: {
            // selectForm(e){

            //     if(e.target.value == ''){
            //         document.getElementById('form_moral').style.display = "none";
            //         document.getElementById('form_fisica').style.display = "none";
            //     }

            //     if(e.target.value == 'Fisica'){
            //         document.getElementById('form_moral').style.display = "none";
            //         document.getElementById('form_fisica').style.display = "block";
            //     }

            //     if(e.target.value == 'Moral'){
            //         document.getElementById('form_moral').style.display = "block";
            //         document.getElementById('form_fisica').style.display = "none";
            //     }
            // },
            getDocuments(){
                axios.get('./getDocuments')
                    .then(response => {
                        console.log(response);
                        this.documents = response.data;
                        this.tableDocuments();
                    });

            },
            tableDocuments(){
                $(document).ready( function () {
                    $('#table_documents').DataTable();
                });
            },
            // deleteClient(client){
            //     let result = window.confirm('¿Desea eliminar este cliente?');

            //     if(result){
            //         axios.get('./deleteClient/'+client)
            //         .then(response => {
            //            if(response.data == 1){
            //             alert('Cliente eliminado');
            //            }else{
            //             alert('Error al eliminar');
            //            }
            //            this.getClients();
            //         });
            //     }else{
            //         return false;
            //     }
                
            // },
            // obtenerImagen(e){
            //     let file = e.target.files[0];
            //     // console.log(file);
            //     this.product.imagen = file;
            //     this.cargarImagen(file);
            // },
            // cargarImagen(file){
            //     let reader = new FileReader();

            //     reader.onload = (e) => {
            //         this.imagenMiniatura = e.target.result;
            //     }

            //     reader.readAsDataURL(file);
            // },
            // updateProduct(){
            //     let person = document.getElementById('type_person').value;

            //     let formData = new FormData();

            //     // if(this.product.name == '' || this.product.stock == ''){
            //     //     alert('Debe rellenar todos los campos');
            //     // }else if(isNaN(this.product.stock)){
            //     //      alert('El campo stock debe ser numerico');
            //     // }else{
            //     //     formData.append('id', this.product.id);
            //     //     formData.append('name', this.product.name);
            //     //     formData.append('stock', this.product.stock);
            //     //     formData.append('imagen', this.product.imagen);

            //     //     axios.post('./updateProduct', formData)
            //     //         .then(response => {
            //     //             // console.log(response.data);
            //     //              alert('Producto actualizado exitosamente');
            //     //             this.getClients();
            //     //         });
            //     // }   

            //     if(person == 'Fisica'){
            //         // console.log(this.client_fisico);
            //        if(this.client_fisico.name == '' || this.client_fisico.phone == '' || this.client_fisico.email == '' || this.client_fisico.rfc == '' || this.client_fisico.curp == '' || this.client_fisico.address == ''){
            //             alert('Debe rellenar todos los campos');
            //         }else{
            //             formData.append('id', this.client_fisico.id);
            //             formData.append('type_person', person);
            //             formData.append('name', this.client_fisico.name);
            //             formData.append('phone', this.client_fisico.phone);
            //             formData.append('email', this.client_fisico.email);
            //             formData.append('rfc', this.client_fisico.rfc);
            //             formData.append('curp', this.client_fisico.curp);
            //             formData.append('address', this.client_fisico.address);
                    
            //             // console.log(formData);
            //             axios.post('../updateClient', formData)
            //                 .then(response => {
            //                     console.log(response.data);
            //                     if(response.data.status == 'error'){
            //                         alert(response.data.msg);
            //                     }

            //                     if(response.data.status == 'success'){
            //                         alert(response.data.msg);
            //                         this.getClients();
            //                         document.getElementById('cerrar').click();
            //                     }
            //                     // alert('Cliente creado exitosamente');
                                
            //             });
            //         }
            //     }

            //     if(person == 'Moral'){
            //        if(this.client_moral.name == '' || this.client_moral.phone == '' || this.client_moral.email == '' || this.client_moral.rfc == '' || this.client_moral.business_name == '' || this.client_moral.address == ''){
            //             alert('Debe rellenar todos los campos');
            //         }else{
            //             formData.append('id', this.client_fisico.id);
            //             formData.append('type_person', person);
            //             formData.append('name', this.client_moral.name);
            //             formData.append('phone', this.client_moral.phone);
            //             formData.append('email', this.client_moral.email);
            //             formData.append('rfc', this.client_moral.rfc);
            //             formData.append('business_name', this.client_moral.business_name);
            //             formData.append('address', this.client_moral.address);
            //             formData.append('turn', this.client_moral.turn);
                    
            //             console.log(formData);
            //             axios.post('../updateClient', formData)
            //                 .then(response => {
            //                     console.log(response.data.msg);

            //                     if(response.data.status == 'error'){
            //                         alert(response.data.msg);
            //                     }

            //                     if(response.data.status == 'success'){
            //                         alert(response.data.msg);
            //                         document.getElementById('cerrar').click();
            //                         this.getClients();
            //                     }
            //                     // alert('Cliente creado exitosamente');
                                
            //             });
            //         }
            //     }
            // },
            // editClient(id_client, type_person){
            //     // console.log(id_client, type_person);

            //     document.getElementById('type_person').value = type_person;

            //     axios.get('./getClient/'+id_client)
            //     .then(response => {
            //         // console.log(response.data);

            //         if(type_person == 'Fisica') {
            //             this.client_fisico = response.data;
            //             document.getElementById('name_fisica').value = response.data.name;
            //             document.getElementById('phone_fisica').value  = response.data.phone;
            //             document.getElementById('email_fisica').value = response.data.email;
            //             document.getElementById('rfc_fisica').value = response.data.rfc;
            //             document.getElementById('curp_fisica').value = response.data.curp;
            //             document.getElementById('address_fisica').value = response.data.address;

            //             document.getElementById('form_moral').style.display = "none";
            //             document.getElementById('form_fisica').style.display = "block";
            //         }

            //         if(type_person == 'Moral') {
            //             this.client_moral = response.data;
            //             document.getElementById('name_moral').value = response.data.name;
            //             document.getElementById('phone_moral').value  = response.data.phone;
            //             document.getElementById('email_moral').value = response.data.email;
            //             document.getElementById('rfc_moral').value = response.data.rfc;
            //             document.getElementById('business_name_moral').value = response.data.business_name;
            //             document.getElementById('address_moral').value = response.data.address;
            //             document.getElementById('turn_moral').value = response.data.turn;

            //             document.getElementById('form_moral').style.display = "block";
            //             document.getElementById('form_fisica').style.display = "none";

            //         }


            //      /*   if(type_person == 'Moral') {
            //             this.client_fisico.name = response.data.name;
            //             this.client_fisico.phone = response.data.phone;
            //             this.client_fisico.email = response.data.email;
            //             this.client_fisico.rfc = response.data.rfc;
            //             this.client_fisico.curp = response.data.curp;
            //             this.client_fisico.address = response.data.address;
            //         }

            //         if(type_person == 'Fisica') {
            //             this.client_fisico.name = response.data.name;
            //             this.client_fisico.phone = response.data.phone;
            //             this.client_fisico.email = response.data.email;
            //             this.client_fisico.rfc = response.data.rfc;
            //             this.client_fisico.business_name = response.data.business_name;
            //             this.client_fisico.address = response.data.address;
            //             this.client_fisico.turn = response.data.turn;
            //         }*/
            //         // this.client.id = response.data.id;
            //         // this.client.name = response.data.name;
            //         // this.client.stock = response.data.stock;

            //         // if(response.data.imagen == null){
            //         //     this.imagenMiniatura = './admin/img/test.png';
            //         // }else{
            //         //     this.imagenMiniatura = response.data.imagen;
            //         // }
                    

            //     });
            // },
        },
        computed: {
            imagen(){
                return this.imagenMiniatura;
            }
        }
    }
</script>

