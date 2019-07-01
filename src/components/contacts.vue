<template>
  <div class="row" id="contacts-container">
    <div class="col-sm-8 m-auto">
      <div class="list-group">
        <div v-bind="contacts" v-for="contact in contacts" :key="contact.id" class="media hvr-underline-from-left">
          <img :src="contact.picture" class="rounded-circle" :alt="contact.firstname" width="100">
          <div class="media-body">
            <h5>{{ contact.firstname }} {{ contact.lastname }}</h5>
            <ul class="list-unstyled">
              <i class="fa fa-envelope-o"></i>
              <li v-for="email in contact.email" :key="email">{{ email }}</li>
            </ul>
            <ul class="list-unstyled">
              <i class="fa fa-phone"></i>
              <li v-for="number in contact.phoneNumber" :key="number">{{ number }}</li>
            </ul>
          </div>
        </div>
        <div class="media" id="not-found-records" v-if="!contacts.length">
          <div class="media-body">
            <p>Sorry, we not fount any contact ... <img src="https://img1.picmix.com/output/stamp/normal/4/4/2/8/528244_739fe.gif" alt="" width="100"></p>
          </div>
        </div>
      </div>
      
    </div>
  </div>
</template>

<script>
export default {
  name: 'Contacts',
  props: {
    contacts: {
      type: Array
    }
  }
}
</script>

<style lang="scss" scoped>
#contacts-container{
  margin-top: 100px;
  margin-bottom: 100px;
  .list-group{
    overflow-y: scroll;
    max-height: calc(100vh - 100px);
    &::-webkit-scrollbar {
      width: 10px;
    }
    &::-webkit-scrollbar-track {
      -webkit-box-shadow: inset 0 0 6px rgba(46, 46, 48, 0.89);
    }
    &::-webkit-scrollbar-thumb {
      background-color: #2098D1;;
      outline: 1px solid #2098D1;;
    }
  }
  .media{
    text-align: left;
    background: rgba(2, 1, 6, .7);
    padding: 20px;
    display: flex;
    align-items: center;
    border-bottom: 1px solid rgba(46, 46, 48, 0.89);
    min-height: 115px;
    cursor: pointer;
    .media-body{
      margin-left: 10px;
      h5{
        color: #fff;
      }
      .list-unstyled{
        margin: 0;
        color: #fff;
        li{
          display: inline;
          margin: 0 5px;
        }
      }
      p{
        color: #fff;
        margin: 0;
      }
    }
  }
}
@media(max-width: 767px) {
  #contacts-container{
    margin-top: 136px;
    .media{
      img{
        width: 50px;
      }
      .media-body{
        h5{
          margin: 0;
        }
        .list-unstyled{
          li{
            font-size: 13px;
            display: none;
            &:first-of-type{
              display: inline-block !important;
            }
          }
          i{
            font-size: 10px;
          }
        }
      }
    }
  }
}
</style>
