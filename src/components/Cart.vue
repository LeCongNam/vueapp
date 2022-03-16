<template>
  <Page>
    <ActionBar title="Giỏ hàng" backgroundColor="#f7f2f6">
      <NavigationButton
        text="Go Back"
        android.systemIcon="ic_menu_back"
        @tap="$navigateBack(App)"
      />
    </ActionBar>
    <!-- chia layout -->
    <GridLayout orientation="vertical" columns="*" rows="*,auto">
        <StackLayout  v-if="this.cart.length==0" >
            <Label text="Không có sản phẩm nào trong giỏ hàng" textWrap="true" />
            <Button text="Về trang chủ" @tap="goBackHome()" />
            
        </StackLayout>

      <StackLayout col="0" row="0">
        <!-- cột sản phẩm -->
        <ListView for="(item,index) in cart">
          <v-template>
            <StackLayout class="card">
              <GridLayout class="card-layout" rows="*" columns="*,*,*,*">
                <Image :src="item.images" row="0" col="0" />
                <StackLayout
                  row="0"
                  colSpan="3"
                  marginLeft="95"
                  marginTop="5"
                  textAlignment="center"
                >
                  <Label :text="'Tên: ' + item.name" fontWeight="bold" />
                  <Label :text="'Mã: ' + item.desc" fontWeight="bold" />
                  <Label :text="'Giá: ' + item.price + '$'" fontWeight="bold" />
                  <Label
                    :text="'Số lượng: ' + item.quantity"
                    fontWeight="bold"
                  />
                </StackLayout>
                <StackLayout row="0" col="3">
                  <GridLayout rows="*,*" columns="*" marginTop="10">
                    <Button
                      text="+"
                      row="0"
                      width="50"
                      height="35"
                      fontSize="12"
                      backgroundColor="#35d411"
                      @tap="plus(item.name,index)"
                    />
                    <Button
                      text="-"
                      row="1"
                      width="50"
                      height="35"
                      fontSize="12"
                      backgroundColor="#35d411"
                      @tap="minus(item.name,index)"
                     
                    />
                  </GridLayout>
                </StackLayout>
              </GridLayout>
            </StackLayout>
          </v-template>
        </ListView>
      </StackLayout>

      <!-- số lượng và tổng -->
      <StackLayout class="count-money" col="0" row="1">
        <GridLayout rows="*,*,*,*" columns="*,100,*,*,*,*,*">
          <Label
            text="Số lượng: "
            row="0"
            col="1"
            marginTop="5"
            fontWeight="bolder"
            fontSize="16"
          />
          <Label :text="itemCount" row="0" col="3" marginTop="5" />
          <Label
            text="Tổng tiền: "
            row="1"
            col="1"
            marginTop="5"
            fontWeight="bolder"
            fontSize="16"
          />
          <Label :text="total + '$'" row="1" col="3" marginTop="5" />
          <Button
            text="Đặt hàng"
            row="2"
            colSpan="3"
            marginLeft="20"
            col="0"
            width="200"
            height="60"
            fontSize="12"
            backgroundColor="#00d4ff"
            @tap="showNow()"
          />
          <Button
            text="Reset"
            row="2"
            col="4"
            colSpan="3"
            marginRight="20"
            width="200"
            height="60"
            fontSize="12"
            backgroundColor="#00d4ff"
            @tap="emptyCart()"
          />
        </GridLayout>
      </StackLayout>
    </GridLayout>
  </Page>
</template>

<script>
import Home from "./App.vue";
export default {
  props: ["cart"],
  data() {
    return {};
  },
  methods: {
    showNow(value) {
      if (this.cart.length > 0) {
        confirm({
          title: "Hệ thống",
          message: "Bạn muốn đặt hàng ngay?",
          okButtonText: "Có",
          cancelButtonText: "Không",
        }).then((res) => {
          if (res) {
            this.clearCart()
            alert("Đã xác nhận đơn hàng");
          }
        });
        return;
      }

      confirm({
        title: "Hệ thống",
        message: "Giỏ hàng trống. Về lại trang chủ?",
        okButtonText: "Có",
        cancelButtonText: "Không",
      }).then((res) => {
        if (res) {
          this.$navigateTo(Home,{
            Animation:true
          });
        }
      });
    },

     clearCart(i) {
          while (this.cart.length != 0) {
            for (i = 0; i < this.cart.length; i++) {
              this.cart.splice(i, 1);
            }
          }        
      }
    ,emptyCart(i) {
      confirm({
        title: "Hệ thống",
        message: "Bạn có muốn xoá giỏ hàng?",
        okButtonText: "Có",
        cancelButtonText: "Không",
      }).then((res) => {
        if (res) {
          while (this.cart.length != 0) {
            for (i = 0; i < this.cart.length; i++) {
              this.cart.splice(i, 1);
            }
          }
        }
      });
    },
    plus(value,index) {
      for (var i = 0; i < this.cart.length; i++) {
        if (index== i) {
          this.cart[index].quantity += 1;
        }
      }
    },
    minus(value,index) {
      for (var i = 0; i < this.cart.length; i++) {
        if (index == i) {
          if (this.cart[i].quantity <= 0) {
            this.cart[index].quantity = 1;
          }
          this.cart[index].quantity -= 1;
        }
      }
    },
    goBackHome(){
      this.$navigateTo(Home,{
        Animation:true
      })
    }
  },
  computed: {
    itemCount() {
      var tongsl = 0;
      for (var i = 0; i < this.cart.length; i++) {
        tongsl += this.cart[i].quantity;
      }
      return tongsl;
    },
    total() {
      var tinhtien = 0;
      for (var i = 0; i < this.cart.length; i++) {
        tinhtien += this.cart[i].quantity * this.cart[i].price;
      }
      return tinhtien;
    },
  },
};
</script>


<style scoped>

.card {
  background-color: #fff;
  color: #4d4d4d;
  margin: 15;
  background-position: center;
}
.card-layout {
  padding: 20;
}
.count-money {
  background-color: rgb(198, 221, 255);
}

.disabled{
    opacity: 0;
    background-color: rgba(0, 0, 0, 0.7);
}
</style>
