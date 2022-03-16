<template>
    <Page>
        <StackLayout class="p-20" backgroundColor="#ffeaa7">
            <Label text="Tên:" marginLeft="10" fontWeight="bold" />
            <TextField style="font-size: 18px; margin-left: 15px;" width="210" />
            <Label text="Số ĐT:" marginLeft="10" fontWeight="bold" />
            <TextField style="font-size: 18px; margin-left: 15px;" width="210" />
            <Button class="btn btn-outline" width="100" text="Xác nhận" @tap="thisModal" />
            <Button class="btn btn-outline" width="100" text="Hủy" @tap="$modal.close" />
        </StackLayout>
    </Page>
</template>

<script>
export default {
    data() {
        return {

        }
    },
    methods: {
        thisModal() {
            alert({
                title: "Tư vấn",
                message: "Lưu lại thành công!",
                okButtonText: "Ok",
            }).then(() => {
                console.log("Alert Dialog Closed");
            });
            this.$modal.close();
        }
    }

}
</script>

<style>