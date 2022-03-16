<template>
  <Page>
    <ActionBar backgroundColor="#f7f2f6" color="#2c3e50">
      <GridLayout rows="*" columns="*,*,*,*,auto">
        <TextField
          width="100%"
          row="0"
          colSpan="3"
          hint="Bạn muốn tìm bài gì?"
          v-model="searchQuery"
        />

        <!--   row="0"
          col="3" -->
        <AbsoluteLayout  row="0"
          col="3">
          <Image
            src="~/assets/images/nvbag.png"
            width="35"
            textAlignment="center"
            @tap="showCart()"
            top="10"
            left="10"
          />
          <Label :text="dem+'+' " backgroundColor="#ffffff" borderRadius="50%" fontSize="20" fontWeight="bold" color="red" top="10" left="30"  @tap="showCart()"/>
        </AbsoluteLayout>

      </GridLayout>
    </ActionBar>
    <!-- end actionbar -->
    <GridLayout columns="*" rows="*,auto">
      <StackLayout>
        <!-- background banner -->
        <StackLayout
          backgroundImage="~/assets/images/banner.jpg"
          borderRadius="10"
          height="130"
          width="90%"
          stretch="aspectFit"
          class="album-image"
        />

        <GridLayout columns="*,*,*,auto" rows="auto">
          <Label
            text="Danh sách sản phẩm"
            row="0"
            colSpan="2"
            fontWeight="bold"
            fontSize="20"
            paddingLeft="10"
            paddingTop="10"
            paddingBottom="10"
            color="#000000"
          />
          <Label
            :text="'Tổng SP(' + countProduct() + ')'"
            row="0"
            col="4"
            fontWeight="bold"
            fontSize="14"
            paddingLeft="10"
            paddingTop="10"
            paddingBottom="10"
            color="#000000"
          />
        </GridLayout>
        <!-- List product -->
        <ListView for="(item, index) in flowerFilter">
          <v-template>
            <StackLayout orientation="horizontal" class="card">
              <GridLayout
                orientation="horizontal"
                class="card-layout"
                rows="*"
                columns="*,200,*"
              >
                <Image
                  :src="item.images"
                  row="0"
                  col="0"
                  @tap="showDetail(item.name,index)"
                />
                <StackLayout row="0" col="1" marginLeft="15" marginTop="15">
                  <Label :text="'Tên: ' + item.name" fontWeight="bold" />
                  <Label :text="'Mã: ' + item.desc" fontWeight="bold" />
                  <Label :text="'Giá: $' + item.price" fontWeight="bold" />
                  <Button
                    text="Thêm"
                    class="btn-add"
                    textAlign="center"
                    row="0"
                    col="2"
                    @tap="addCart(item,index)"
                  />
                </StackLayout>
              </GridLayout>
            </StackLayout>
          </v-template>
        </ListView>
                <!-- end Products -->
          
      </StackLayout>
      
    </GridLayout>
  </Page>
</template>

<script >
import showCategory from "./showCategory.vue";
import Detail from "./Deatail.vue";
import Cart from "./Cart.vue";

export default {
  props: ["user"],
  data() {
    return {
      Products: [
        {
          images: "~/assets/images/mac1.jpg",
          desc: "NG745",
          name: "Apple MacBook Pro 13 ",
          price: 26,
          quantity:1,
          enable: false,
          details:"Bên cạnh sử dụng con chip mới Apple còn ra mắt phiên bản hệ điều hành macOS Big Sur với giao diện hoàn hảo hơn, các chuyển động cuộn, phóng to và chuyển tiếp màn hình mượt mà. Ngoài đổi mới giao diện macOS Big Sur còn mang đến khả năng phản hồi nhanh chóng và kho ứng dụng khổng lồ.",

        },
        {
          images: "~/assets/images/mac5.jpg",
          desc: "NG774",
          name: "Macbook Pro 14 inch 2021 ",
          price: 20,
          quantity:1,
          enable: true,
          details:"Bên cạnh sử dụng con chip mới Apple còn ra mắt phiên bản hệ điều hành macOS Big Sur với giao diện hoàn hảo hơn, các chuyển động cuộn, phóng to và chuyển tiếp màn hình mượt mà. Ngoài đổi mới giao diện macOS Big Sur còn mang đến khả năng phản hồi nhanh chóng và kho ứng dụng khổng lồ.",

        },
        {
          images: "~/assets/images/mac14.jpg",
          desc: "NG732",
          name: "Macbook Pro 14 inch 2021 ",
          price: 50,
          quantity:1,
          enable: true,
          details:"Bên cạnh sử dụng con chip mới Apple còn ra mắt phiên bản hệ điều hành macOS Big Sur với giao diện hoàn hảo hơn, các chuyển động cuộn, phóng to và chuyển tiếp màn hình mượt mà. Ngoài đổi mới giao diện macOS Big Sur còn mang đến khả năng phản hồi nhanh chóng và kho ứng dụng khổng lồ.",

        },
        {
          images: "~/assets/images/mac2.jpg",
          desc: "NG787",
          name: "Macbook Pro 14 inch 2021 ",
          price: 43,
          quantity:1,
          enable: true,
          details:"Bên cạnh sử dụng con chip mới Apple còn ra mắt phiên bản hệ điều hành macOS Big Sur với giao diện hoàn hảo hơn, các chuyển động cuộn, phóng to và chuyển tiếp màn hình mượt mà. Ngoài đổi mới giao diện macOS Big Sur còn mang đến khả năng phản hồi nhanh chóng và kho ứng dụng khổng lồ.",

        },
        {
          images: "~/assets/images/mac13.jpg",
          desc: "NG789",
          name: "Apple MacBook Pro 13 ",
          price: 27,
          quantity:1,
          enable: true,
          details:"Bên cạnh sử dụng con chip mới Apple còn ra mắt phiên bản hệ điều hành macOS Big Sur với giao diện hoàn hảo hơn, các chuyển động cuộn, phóng to và chuyển tiếp màn hình mượt mà. Ngoài đổi mới giao diện macOS Big Sur còn mang đến khả năng phản hồi nhanh chóng và kho ứng dụng khổng lồ.",

        },
        {
          images: "~/assets/images/mac4.jpg",
          desc: "NG798",
          name: "Macbook Pro 16 inch 2021",
          price: 43,
          quantity:1,
          enable: true,
          details:"Bên cạnh sử dụng con chip mới Apple còn ra mắt phiên bản hệ điều hành macOS Big Sur với giao diện hoàn hảo hơn, các chuyển động cuộn, phóng to và chuyển tiếp màn hình mượt mà. Ngoài đổi mới giao diện macOS Big Sur còn mang đến khả năng phản hồi nhanh chóng và kho ứng dụng khổng lồ.",

        },
        {
          images: "~/assets/images/mac14.jpg",
          desc: "NG747",
          name: "Macbook Pro 14 M1 Pro 10 CPU - ",
          price: 32,
          quantity:1,
          enable: true,
          details:"Bên cạnh sử dụng con chip mới Apple còn ra mắt phiên bản hệ điều hành macOS Big Sur với giao diện hoàn hảo hơn, các chuyển động cuộn, phóng to và chuyển tiếp màn hình mượt mà. Ngoài đổi mới giao diện macOS Big Sur còn mang đến khả năng phản hồi nhanh chóng và kho ứng dụng khổng lồ.",

        },
        {
          images: "~/assets/images/mac3.jpg",
          desc: "NG781",
          name: "Macbook Pro 14 M1 Pro ",
          price: 39,
          quantity:1,
          enable: true,
          details:"Bên cạnh sử dụng con chip mới Apple còn ra mắt phiên bản hệ điều hành macOS Big Sur với giao diện hoàn hảo hơn, các chuyển động cuộn, phóng to và chuyển tiếp màn hình mượt mà. Ngoài đổi mới giao diện macOS Big Sur còn mang đến khả năng phản hồi nhanh chóng và kho ứng dụng khổng lồ.",

        },
        {
          images: "~/assets/images/mac6.jpg",
          desc: "NG748",
          name: "Macbook Pro 16 inch 2021 ",
          price: 32,
          quantity:1,
          enable: true,
          details:"Bên cạnh sử dụng con chip mới Apple còn ra mắt phiên bản hệ điều hành macOS Big Sur với giao diện hoàn hảo hơn, các chuyển động cuộn, phóng to và chuyển tiếp màn hình mượt mà. Ngoài đổi mới giao diện macOS Big Sur còn mang đến khả năng phản hồi nhanh chóng và kho ứng dụng khổng lồ.",

        },
        {
          images: "~/assets/images/mac7.jpg",
          desc: "NG759",
          name: "Macbook Pro 14 inch 2021",
          price: 39,
          quantity:1,
          enable: true,
          details:"Bên cạnh sử dụng con chip mới Apple còn ra mắt phiên bản hệ điều hành macOS Big Sur với giao diện hoàn hảo hơn, các chuyển động cuộn, phóng to và chuyển tiếp màn hình mượt mà. Ngoài đổi mới giao diện macOS Big Sur còn mang đến khả năng phản hồi nhanh chóng và kho ứng dụng khổng lồ.",

        },
        {
          images: "~/assets/images/mac1.jpg",
          desc: "NG791",
          name: "Macbook Pro 14 M1 Pro ",
          price: 25,
          quantity:1,
          enable: true,
          details:"Bên cạnh sử dụng con chip mới Apple còn ra mắt phiên bản hệ điều hành macOS Big Sur với giao diện hoàn hảo hơn, các chuyển động cuộn, phóng to và chuyển tiếp màn hình mượt mà. Ngoài đổi mới giao diện macOS Big Sur còn mang đến khả năng phản hồi nhanh chóng và kho ứng dụng khổng lồ.",

        },
        {
          images: "~/assets/images/mac8.jpg",
          desc: "NG738",
          name: "Macbook Pro 16 inch 2021",
          price: 45,
          quantity:1,
          enable: true,
          details:"Bên cạnh sử dụng con chip mới Apple còn ra mắt phiên bản hệ điều hành macOS Big Sur với giao diện hoàn hảo hơn, các chuyển động cuộn, phóng to và chuyển tiếp màn hình mượt mà. Ngoài đổi mới giao diện macOS Big Sur còn mang đến khả năng phản hồi nhanh chóng và kho ứng dụng khổng lồ.",

        },
        {
          images: "~/assets/images/mac9.jpg",
          desc: "NG785",
          name: "Macbook Pro 14 M1 Pro ",
          price: 25,
          quantity:1,
          enable: true,
          details:"Bên cạnh sử dụng con chip mới Apple còn ra mắt phiên bản hệ điều hành macOS Big Sur với giao diện hoàn hảo hơn, các chuyển động cuộn, phóng to và chuyển tiếp màn hình mượt mà. Ngoài đổi mới giao diện macOS Big Sur còn mang đến khả năng phản hồi nhanh chóng và kho ứng dụng khổng lồ.",

        },
        {
          images: "~/assets/images/mac10.jpg",
          desc: "NG765",
          name: "Macbook Pro 14 inch 2021 ",
          price: 25,
          quantity:1,
          enable: true,
          details:"Bên cạnh sử dụng con chip mới Apple còn ra mắt phiên bản hệ điều hành macOS Big Sur với giao diện hoàn hảo hơn, các chuyển động cuộn, phóng to và chuyển tiếp màn hình mượt mà. Ngoài đổi mới giao diện macOS Big Sur còn mang đến khả năng phản hồi nhanh chóng và kho ứng dụng khổng lồ.",

        },
        {
          images: "~/assets/images/mac6.jpg",
          desc: "NG759",
          name: "Apple MacBook Pro 13 ",
          price: 17,
          quantity:1,
          enable: true,
          details:"Bên cạnh sử dụng con chip mới Apple còn ra mắt phiên bản hệ điều hành macOS Big Sur với giao diện hoàn hảo hơn, các chuyển động cuộn, phóng to và chuyển tiếp màn hình mượt mà. Ngoài đổi mới giao diện macOS Big Sur còn mang đến khả năng phản hồi nhanh chóng và kho ứng dụng khổng lồ.",

        },
        {
          images: "~/assets/images/mac11.jpg",
          desc: "NG763",
          name: "Macbook Pro 14 inch 2021",
          price: 22,
          quantity:1,
          enable: true,
          details:"Bên cạnh sử dụng con chip mới Apple còn ra mắt phiên bản hệ điều hành macOS Big Sur với giao diện hoàn hảo hơn, các chuyển động cuộn, phóng to và chuyển tiếp màn hình mượt mà. Ngoài đổi mới giao diện macOS Big Sur còn mang đến khả năng phản hồi nhanh chóng và kho ứng dụng khổng lồ.",

        },
        {
          images: "~/assets/images/mac12.jpg",
          desc: "NG743",
          name: "Macbook Pro 16 inch 2021 ",
          price: 14,
          quantity:1,
          enable: true,
          details:"Bên cạnh sử dụng con chip mới Apple còn ra mắt phiên bản hệ điều hành macOS Big Sur với giao diện hoàn hảo hơn, các chuyển động cuộn, phóng to và chuyển tiếp màn hình mượt mà. Ngoài đổi mới giao diện macOS Big Sur còn mang đến khả năng phản hồi nhanh chóng và kho ứng dụng khổng lồ.",

        },
        {
          images: "~/assets/images/mac10.jpg",
          desc: "NG716",
          name: "Macbook Pro M1 Pro 16 10 CPU - ",
          price: 30,
          quantity:1,
          enable: true,
          details:"Bên cạnh sử dụng con chip mới Apple còn ra mắt phiên bản hệ điều hành macOS Big Sur với giao diện hoàn hảo hơn, các chuyển động cuộn, phóng to và chuyển tiếp màn hình mượt mà. Ngoài đổi mới giao diện macOS Big Sur còn mang đến khả năng phản hồi nhanh chóng và kho ứng dụng khổng lồ.",

        },
      ],
      cart: [],
      searchQuery: null,
      quantityProduct: 0,
      dem: 0,
    };
  },
  methods: {
    showCategory(item) {
      this.$navigateTo(showCategory, {
        props: {
          data: item,
        },
      });
    },

    showDetail(name,index) {
      var index;
      for (var i = 0; i < this.Products.length; i++) {
        if (name == this.Products[i].name) {
          index = i;
        }
      }
      this.$navigateTo(Detail, {
        props: {
          images: this.Products[index].images,
          name: this.Products[index].name,
          desc: this.Products[index].desc,
          price: this.Products[index].price,
          details:this.Products[index].details,

        },
      });
    },
    showCart() {
      this.$navigateTo(Cart, {
        props: {
          cart: this.cart,
        },
      });
    },
    addCart(obj,index) {
      this.dem++;
      var flag = false;
      if (this.cart.length < 0) {
        flag = true;
      } else {
        for (let i = 0; i < this.cart.length; i++) {
          if (index== i) {
            flag = true;
          }
        }
      }
      if (flag == false) {
        this.cart.push(obj);
      } else {
        for (var i = 0; i < this.cart.length; i++) {
          if (index== i) {
            this.cart[i].quantity += 1;
          }
        }
      }
    },
    countProduct() {
      return this.Products.length;
    },
  },
  computed: {
    flowerFilter() {
      var name = this.searchQuery;
      var list = this.Products;
      if (name == null) {
        return list;
      }
      name = name.trim().toUpperCase();
      list = list.filter(function (obj) {
        if (obj.name.toUpperCase().indexOf(name) != -1) {
          return obj;
        }
      });
      return list;
    },
    Count() {
      var tongsl = 0;
      for (var i = 0; i < this.cart.length; i++) {
        tongsl += this.cart[i].quantity;
      }
      return tongsl;
    },
  },
};
</script>

<style scoped>
.album-image {
  background-repeat: no-repeat;
  background-size: cover;
  background-position: center;
}
.card {
  background-color: #fff;
  color: #4d4d4d;
  margin: 15;
  background-position: center;
}
.card-layout {
  padding: 20;
}
.count {
  width: 20;
  height: 20;
  background-color: #e76f51;
  border-radius: 25rem;
  text-align: center;
  align-items: center;
  margin-left: 2;
  margin-bottom: 20;
  color: white;
  opacity: 1;
}

.btn-add {
  width: 60;
  font-size: 9;
  height: 30;
  margin-right: 20px;
  background-color: #c85dfa;
  border-top-right-radius: 10px;
  border-top-left-radius: 4px;
  border-bottom-left-radius: 10px;
  border-bottom-right-radius: 4px;
}
</style>
