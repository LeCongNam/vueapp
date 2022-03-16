<template>
    <Page>
        <ActionBar title="Chi tiết" backgroundColor="#f7f2f6">
          <NavigationButton text="Go Back" android.systemIcon="ic_menu_back" @tap="$navigateBack(App)" />
        </ActionBar>
        <GridLayout rows="auto,*" colums="*">
            <GridLayout col="0" row="0" rows="300,*,*,*,*,*,*" columns="*,*,*">
                <Image :src="images" width="100%" row="0" marginBottom="10" colSpan="3" />
                <Label :text="'Tên: ' + name" row="1" fontWeight="bold" fontSize="16" marginLeft="20" colSpan="2" />
                <Label :text="'Mã: ' + desc" row="2" fontWeight="bold" fontSize="16" marginLeft="20" colSpan="2" />
                <Label :text="'Giá: ' + price+'$'" row="3" fontWeight="bold" fontSize="16" marginLeft="20" colSpan="2" />
            </GridLayout>

            <StackLayout row="1" col="0">
               <Label text="Thông tin chi tiết sản phẩm:" fontWeight="bold" fontSize="16"  marginLeft="20"  textWrap="true"  />
                <Label :text="details"  fontSize="16" marginLeft="20" class="grap"   textWrap="true" />
            </StackLayout>
        </GridLayout>
    </Page>
</template>

<script>
export default {
    props: ['images', 'name', 'desc', 'price','details'],
    data() {
        return {}
    },
    methods: {
        
    }
}
</script>

<style scoped>
    .grap{
        margin-right: 20;
        line-height: 1.6;
    }
</style>