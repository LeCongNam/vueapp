<template>
    <Page>
        <ActionBar title="Chi tiết" backgroundColor="#f7f2f6">
          <NavigationButton text="Go Back" android.systemIcon="ic_menu_back" @tap="$navigateBack(App)" />
        </ActionBar>
        <StackLayout orientation="horizontal">
            <GridLayout rows="300,*,*,*,*,*,*,*" columns="*,*,*">
                <Image :src="data.images" width="100%" row="0" marginBottom="10" colSpan="3" />
                <Label :text="'Tên: ' + data.name" row="1" fontWeight="bold" fontSize="16" marginLeft="20" colSpan="2" />
                <Label :text="'Giá: ' + data.price+'$'" row="2" fontWeight="bold" fontSize="16" marginLeft="20" colSpan="2" />
                <Button text="Tư vấn" row="1" col="2" fontSize="13" width="85" borderRadius="24" height="40" backgroundColor="#fc9493" marginTop="30" marginRight="20" @tap="show" />
            </GridLayout>
        </StackLayout>
    </Page>
</template>

<script>
 import Consult from './Consult.vue'
export default {
    props: ['data'],
    data() {
        return {

        }
    },
    methods: {
        show() {
            this.$showModal(Consult).then((data) => {
                this.provinces.push(data);
                this.$refs.listview.refresh();
            })
        }
    }    
}
</script>