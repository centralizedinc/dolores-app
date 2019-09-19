<template>
<a-row type="flex" :gutter="3"  >
    <a-col :span="8 "  style="margin-top:1vh; text-align: center">
        <a-card bodyStyle="background-color:#c8d5b9" hoverable>
            <template class="ant-card-actions" slot="actions">
                <a-tooltip placement="top">
                    <template slot="title">
                        <span>Apply</span>
                    </template>
                    <a-icon type="edit" @click="redirect('business-permit')"/>
                </a-tooltip>
            </template>

            <a-card-meta title="Mayor's Permit" description="or Business Permit for every company and business ">
            </a-card-meta>
        </a-card>
    </a-col>
    <a-col :span="8 "style="margin-top:1vh; text-align: center">
       <a-card bodyStyle="background-color:#c8d5b9" hoverable>
            <template class="ant-card-actions" slot="actions">
                <a-tooltip placement="top">
                    <template slot="title">
                        <span>Apply</span>
                    </template>
                    <a-icon type="edit" />
                </a-tooltip>
            </template>

            <a-card-meta title="Sanitary Permit" description="Food and Non-food business establishments">
            </a-card-meta>
        </a-card>
    </a-col>
     <a-col :span="8 " style="margin-top:1vh; text-align: center">
       <a-card bodyStyle="background-color:#c8d5b9" hoverable>
            <template class="ant-card-actions" slot="actions">
                <a-tooltip placement="top">
                    <template slot="title">
                        <span>Apply</span>
                    </template>
                    <a-icon type="edit" />
                </a-tooltip>
            </template>

            <a-card-meta title="Occupancy Permit" description="(Mayor's Permit)">
            </a-card-meta>
        </a-card>
    </a-col>
    <!-- <a-col :span="8 "style="margin-top:1vh; text-align: center">
       <a-card bodyStyle="background-color:#c8d5b9" hoverable>
            <template class="ant-card-actions" slot="actions">
                <a-tooltip placement="top">
                    <template slot="title">
                        <span>Apply</span>
                    </template>
                    <a-icon type="edit" />
                </a-tooltip>
            </template>

            <a-card-meta title="Other Permits" description="(Mayor's Permit)">
            </a-card-meta>
        </a-card>
    </a-col> -->
    <a-col :span="8 " style="margin-top:1vh; text-align: center">
       <a-card bodyStyle="background-color:#c8d5b9" hoverable>
            <template class="ant-card-actions" slot="actions">
                <a-tooltip placement="top">
                    <template slot="title">
                        <span>Apply</span>
                    </template>
                    <a-icon type="edit" />
                </a-tooltip>
            </template>

            <a-card-meta title="Applied Permit" description="Check status of application">
            </a-card-meta>
        </a-card>
    </a-col>
   
</a-row>
</template>

<script>
export default {};
</script>

<style>
.permitButtons {
    height: 10vh;
    background-color: #c8d5b9 !important;
    border-color: #faf3dd !important;
    color: #000000 !important;
}
</style>
