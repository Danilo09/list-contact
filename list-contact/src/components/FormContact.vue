<template>
    <div class="row">
        <div class="col-12 border-bottom mb-5 d-flex justify-content-between align-items-center">
            <!-- <h2 :title="ex">{{name}}</h2> -->
            <!-- <p>{{contactsCount}}</p> -->
        </div>

        <div class="col-12 col-lg-4 form-contact">

            <form action="">

                <div class="form-group mr-1">
                    <label>Nome</label>
                    <input type="text" class="form-control" placeholder="Nome Completo..." v-model="contact.name">
                </div>

                <div class="form-group mr-1">
                    <label>Cpf</label>
                    <input type="text" class="form-control" placeholder="Informe o CPF" v-model="contact.cpf">
                </div>


                <div class="form-group mr-1">
                    <label>E-mail</label>
                    <input type="email" class="form-control" placeholder="Seu melhor email..." v-model="contact.email">
                </div>

                <div class="form-group mr-1">
                    <label>Contato</label>
                    <input type="phone" class="form-control" placeholder="Telefone/Celular" v-model="contact.phone">
                </div>

                <div class="form-group ml-1">
                    <button v-if="!isEdit" class="btn btn-lg btn-rounded btn-success" @click.prevent="saveContact(contact)">Criar Contato</button>
                    <button v-if="isEdit" class="btn btn-lg btn-rounded btn-primary" @click.prevent="updateContact(contact)">Atualizar Contato</button>
                </div>
            </form>
        </div>

        <div class="col-8 border-left">
            
            <div class="contact" v-if="contacts">
                    
                <div class="col-12 mb-2" v-for="contact in contacts" v-bind:key="contact.key">

                    <div class="card">
                        <div class="card-body">
                            <h5 class="card-title">Nome:{{contact.name}}</h5>

                            <p class="card-text">CPF: {{ contact.cpf}}</p>
                            <p class="card-text">E-mail: {{contact.email}}</p>
                            <p class="card-text">Telefone: {{contact.phone}}</p>

                            <a href="#" class="btn btn-sm btn-primary" @click.prevent="editContact(contact)">EDITAR</a>
                            <a href="#" class="btn btn-sm btn-danger" @click.prevent="removeContact(contact.id)">DELETAR</a>
                        </div>

                    </div>
                </div>

            </div>
            <!-- <div v-else>Nenhum contato encontrado!</div> -->
        </div>
    </div>
</template>

<script>
import axios from "axios"
export default {
  name: 'FormContact',
  props: {
  },
  data() {
    return {
      contacts: [],
      contactsResponse: [],
      name: 'Contatos App',
      contact: {
          id: null,
          name: '',
          cpf: '',
          email: '',
          phone: ''
      },
      isEdit: false,
      ex: 'Meu app de contatos'
    }
  },
      computed: {
        contactsCount() {
            return `Total de contatos é ${this.contacts.length}`;
        }
    },
    mounted () {
    var newContacts
      axios
        .get('https://private-21e8de-rafaellucio.apiary-mock.com/users')
        .then(response => (
                this.contactsResponse = response.data,
                newContacts = this.contactsResponse,
                Object.keys(newContacts).map(
                    function(object){
                    newContacts[object]["id"]= new Date().getTime();
                }),

                localStorage.setItem("contac", JSON.stringify(newContacts)),

                this.contact = newContacts
            ))
    },
    created() {
        this.contacts = JSON.parse(localStorage.getItem('contactsApp'));
    },
    methods: {
        saveContact(contact) {

            let contacts = localStorage.getItem('contactsApp');

            contact.id = new Date().getTime();

            if(contacts) {
                
                contacts = JSON.parse(contacts);
                contacts.push(contact);

            } else {
                contacts = [contact];
            }

            this.contacts = contacts;

            // o atualizar local storage independemente de novo contato ou nova adição   
            localStorage.setItem('contactsApp', JSON.stringify(contacts));

            location.reload();
        },
        removeContact(contactId) {
            let contacts = localStorage.getItem('contactsApp');

            if(!contacts) return;

            contacts = JSON.parse(contacts);

            contacts = contacts.filter((contact) => {
                return contact.id != contactId;
            });

            this.contacts = contacts;

            localStorage.setItem('contactsApp', JSON.stringify(contacts));
        },
        editContact(contact) {
            this.contact = contact;
            this.isEdit = true;
        },
        updateContact(contact) {
            let contacts = this.contacts.map(contactMap => {
                if(contactMap.id == contact.id) {
                    return contact;
                }

                return contactMap;
            });

            this.contacts = contacts;
            this.isEdit = false;

            localStorage.setItem('contactsApp', JSON.stringify(contacts));

            location.reload();

        }
    }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>
