<template>
  <a-card title="hello">
    <a-table :columns="cols" :dataSource="transac">
      <template slot="permit" slot-scope="text">
        <a href="javascript:;">{{text}}</a>
        <a slot="action" slot-scope="text" href="javascript:;" @click="view_data">View</a>
      </template>
      <template slot="application.app_type" slot-scope="text, record">
        <p v-if="text == 1">New</p>
        <p v-else>Renewal</p>
      </template>
      <template slot="action" slot-scope="text, record, index">
        <div>
          <a @click="() => view_data(record)">View</a>
        </div>
      </template>
      <template slot="title">All Permit Transaction</template>
    </a-table>
    <a-drawer width="75%" placement="right" :closable="false" @close="onClose" :visible="draw_show">
      <a-menu v-model="current" mode="horizontal">
        <a-menu-item key="permit">Permit</a-menu-item>
        <a-menu-item key="insurance">Insurance</a-menu-item>
        <a-menu-item key="payment">Payment</a-menu-item>
      </a-menu>
      <a-card style="textAlign:'center'" v-show="current =='permit'">
        <a-row>
          <div align="center">
            <p>
              Republic of the Philippines
              <br />Dolores Quezon
              <br />OFFICE OF THE MAYOR
              <br />
              {{form.application.permit_type}} and Licensing Office
              <br />Telephone no. +63 42 710-8892
              <br />
              <br />Application:
              <u v-if="form.application.app_type == 1">New</u>
              <u v-else>Renewal</u>
            </p>
          </div>
        </a-row>
        <!-- <p>Permit Details</p>
        <p>{{form.application.permit_type}}</p>-->
        <a-row>
          <!-- <a-col :span="12">
          <a-form-item label="Permit Type: " :label-col="{ span: 8 }">-->
          <!-- <a-input
              disabled="true"
              v-model="form.application.permit_type"
          ></a-input>-->
          <!-- <u>{{form.application.permit_type}}</u>
            </a-form-item>
          </a-col>-->

          <a-col :span="12">
            <p class="inset">Date of Application in PBR: {{form.application.pbr_date}}</p>
            <!-- <p>Application: {{form.application.app_type}}</p> -->
            <!-- <a-form-item label="Application">
                <p></p>
            </a-form-item>-->
          </a-col>
          <a-col :span="12">
            <!-- <p class="dashed">Date of Application in PBR: {{form.application.pbr_date}}</p> -->
            <p class="inset">Date of Application in LGU: {{form.application.lgu_date}}</p>
            <!-- <a-form-item label="pbr_date" :label-col="{ span: 8 }" :wrapper-col="{ span: 16 }">
              <p>{{form.application.pbr_date}}</p>
            </a-form-item>-->
          </a-col>
        </a-row>
        <a-row>
          <!-- <a-col :span="12">
            <a-form-item label="lgu_date" :label-col="{ span: 8 }" :wrapper-col="{ span: 16 }">
              <p>{{form.application.lgu_date}}</p>
            </a-form-item>
          </a-col>-->
          <a-col :span="12" style="margin-top:-15px">
            <p class="inset">Reference No./B.I.N.: {{form.application.reference_no}}</p>

            <!-- <a-form-item label="reference_no" :label-col="{ span: 8 }" :wrapper-col="{ span: 16 }">
              <p>{{form.application.reference_no}}</p>
            </a-form-item>-->
          </a-col>
          <a-col :span="12" style="margin-top:-15px">
            <p class="inset">DTI/SEC/CDA Registration No.: {{form.application.registration_no}}</p>
            <!-- <a-form-item
              label="registration_no"
              :label-col="{ span: 8 }"
              :wrapper-col="{ span: 16 }"
            >
              <p>{{form.application.registration_no}}</p>
            </a-form-item>-->
          </a-col>
        </a-row>
        <a-row>
          <!-- business -->
          <a-col :span="14" style="margin-top:-15px">
            <p class="inset">
              Kind of Ownership:
              <a-radio-group v-model="form.business.ownership" disabled="true">
                <a-radio :value="1">Sole Proprietorship</a-radio>
                <a-radio :value="2">Partnership</a-radio>
                <a-radio :value="3">Corporation</a-radio>
              </a-radio-group>
            </p>

            <!-- <a-form-item label="ownership" :label-col="{ span: 8 }" :wrapper-col="{ span: 16 }">
              <p>{{form.business.ownership}}</p>
            </a-form-item>-->
          </a-col>
          <a-col :span="5" style="margin-top:-15px">
            <p class="inset">TIN: {{form.business.tin}}</p>
            <!-- <a-form-item label="tin" :label-col="{ span: 8 }" :wrapper-col="{ span: 16 }">
              <p>{{form.business.tin}}</p>
            </a-form-item>-->
          </a-col>
          <a-col :span="5" style="margin-top:-15px">
            <p class="inset">SSS No.: {{form.business.sss}}</p>
            <!-- <a-form-item label="sss" :label-col="{ span: 8 }" :wrapper-col="{ span: 16 }">
              <p>{{form.business.sss}}</p>
            </a-form-item>-->
            <!-- <description-item title="Business Name: ">{{form.business_name}}</description-item> -->
          </a-col>
        </a-row>
        <a-row>
          <a-col :span="12" style="margin-top:-15px">
            <p class="inset">Business Name: {{form.business.business_name}}</p>
            <!-- <a-form-item label="business_name" :label-col="{ span: 8 }" :wrapper-col="{ span: 16 }">
              <p>{{form.business.business_name}}</p>
            </a-form-item>-->
          </a-col>
          <a-col :span="12" style="margin-top:-15px">
            <p class="inset">Name of Applicant/Owner/Manager: {{form.business.amo.name}}</p>
          </a-col>
        </a-row>
        <a-row type="flex">
          <a-col :span="12" style="margin-top:-15px">
            <p class="inset">Business Address: {{form.business.business_address}}</p>
            <!-- <a-form-item
              label="business_address"
              :label-col="{ span: 8 }"
              :wrapper-col="{ span: 16 }"
            >
              <p>{{form.business.business_address}}</p>
            </a-form-item>-->
          </a-col>
          <a-col :span="12" style="margin-top:-15px">
            <p class="inset">Applicant's/Owner's/Manager's Address: {{form.business.amo.address}}</p>
          </a-col>
        </a-row>
        <a-row>
          <a-col :span="12" style="margin-top:-15px">
            <p class="inset">Business Contact No.: {{form.business.contact}}</p>
            <!-- <a-form-item label="contact" :label-col="{ span: 8 }" :wrapper-col="{ span: 16 }">
              <p>{{form.business.contact}}</p>
            </a-form-item>-->
          </a-col>
          <a-col :span="12" style="margin-top:-15px">
            <p class="inset">Applicant's/Owner's/Manager's Contact: {{form.business.amo.contact}}</p>
            <!-- <a-form-item
              label="applicant/manager/owner contact"
              :label-col="{ span: 8 }"
              :wrapper-col="{ span: 16 }"
            >
              <p>{{form.business.amo.contact}}</p>
            </a-form-item>-->
          </a-col>
        </a-row>
        <a-row>
          <a-col :span="12" style="margin-top:-15px">
            <p class="inset">Business E-mail: {{form.business.email}}</p>
            <!-- <a-form-item label="email" :label-col="{ span: 8 }" :wrapper-col="{ span: 16 }">
              <p>{{form.business.email}}</p>
            </a-form-item>-->
            <!-- <description-item title="Business Address">{{form.business_address}}</description-item> -->
          </a-col>
          <a-col :span="12" style="margin-top:-15px">
            <p class="inset">Applicant's/Owner's/Manager's E-mail: {{form.business.amo.email}}</p>
            <!-- <a-form-item
              label="applicant/manager/owner email"
              :label-col="{ span: 8 }"
              :wrapper-col="{ span: 16 }"
            >
              <p>{{form.business.amo.email}}</p>
            </a-form-item>-->
          </a-col>
        </a-row>
        <a-row>
          <a-col :span="6" style="margin-top:-15px">
            <p class="inset">Business Area (in sq m): {{form.business.business_area}}</p>
            <!-- <a-form-item label="business_area" :label-col="{ span: 8 }" :wrapper-col="{ span: 16 }">
              <p>{{form.business.business_area}}</p>
            </a-form-item>-->
          </a-col>
          <a-col :span="6" style="margin-top:-15px">
            <p class="inset">No. of Owners: {{form.businessowner_no}}</p>
            <!-- <a-form-item label="owner_no" :label-col="{ span: 8 }" :wrapper-col="{ span: 16 }">
              <p>{{form.businessowner_no}}</p>
            </a-form-item>-->
          </a-col>
          <a-col :span="12" style="margin-top:-15px">
            <p class="inset">
              No. of Employees:
              <u>{{form.business.employees_no.professional}}</u> Professional
              <u>{{form.business.employees_no.non_professional}}</u> Non-Professional
            </p>
            <!-- <a-form-item
              label="employees_no professional"
              :label-col="{ span: 8 }"
              :wrapper-col="{ span: 16 }"
            >
              <p>{{form.business.employees_no.professional}}</p>
            </a-form-item>-->
          </a-col>
          <!-- <a-col :span="6">
            <a-form-item
              label="employees_no non_professional"
              :label-col="{ span: 8 }"
              :wrapper-col="{ span: 16 }"
            >
              <p>{{form.business.employees_no.non_professional}}</p>
            </a-form-item>
          </a-col>-->
        </a-row>
        <a-row>
          <a-col :span="24" style="margin-top:-15px">
            <p class="inset">
              <a-radio-group v-model="form.business.business_type" disabled="true">
                <a-radio :value="1">Rented</a-radio>
                <a-radio :value="2">Owned</a-radio>
              </a-radio-group>If place of business is RENTED, please identify the following
            </p>
            <!-- <a-form-item label="business_type" :label-col="{ span: 8 }" :wrapper-col="{ span: 16 }">
              <p>{{form.business.business_type}}</p>
            </a-form-item>-->
          </a-col>
        </a-row>
        <a-row>
          <!-- if rented -->
          <a-col :span="12" style="margin-top: -15px">
            <p class="inset">Lessor's Name: {{form.business.rented.lessor}}</p>
            <!-- <a-form-item label="rented lessor" :label-col="{ span: 8 }" :wrapper-col="{ span: 16 }">
              <p>{{form.business.rented.lessor}}</p>
            </a-form-item>-->
          </a-col>
          <a-col :span="12" style="margin-top: -15px">
            <p class="inset">Monthly Rental: {{form.business.rented.monthly_rental}}</p>
            <!-- <a-form-item
              label="rented monthly_rental"
              :label-col="{ span: 8 }"
              :wrapper-col="{ span: 16 }"
            >
              <p>{{form.business.rented.monthly_rental}}</p>
            </a-form-item>-->
          </a-col>
        </a-row>
        <a-row>
          <a-col :span="24" style="margin-top: -15px">
            <p class="inset">Lessor's Address: {{form.business.rented.lessor_address}}</p>
            <!-- <a-form-item
              label="rented lessor_address"
              :label-col="{ span: 8 }"
              :wrapper-col="{ span: 16 }"
            >
              <p>{{form.business.rented.lessor_address}}</p>
            </a-form-item>-->
          </a-col>
        </a-row>
        <a-row>
          <a-col :span="12" style="margin-top: -15px">
            <p class="inset">Telephone No.: {{form.business.rented.lessor_contact}}</p>
          </a-col>
          <a-col :span="12" style="margin-top: -15px">
            <p class="inset">E-mail Address: {{form.business.rented.lessor_email}}</p>
          </a-col>
        </a-row>
        <a-row>
          <a-col :span="24" style="margin-top: -15px">
            <p class="inset">
              Property Index Number (P.I.N.) Real Property Information: Land
              <u>{{form.business.property_pin.land}}</u> Building
              <u>{{form.business.property_pin.building}}</u> Machinery
              <u>{{form.business.property_pin.machinery}}</u>
            </p>
          </a-col>
        </a-row>
        <a-row>
          <a-col :span="24" style="margin-top: -15px">
            <p class="inset">Business Activity(ies)</p>
          </a-col>
          <a-col :span="8" style="margin-top: -15px">
            <p class="inset">Line of Business</p>
          </a-col>
          <a-col :span="8" style="margin-top: -15px">
            <p class="inset">Capitalization</p>
          </a-col>
          <a-col :span="8" style="margin-top: -15px">
            <p class="inset">Gross Sales/Receipts</p>
          </a-col>
        </a-row>
        <a-row v-for="i in form.business.business_activities.length" :key="i=0">
          <!-- <a-table :columns="columns" :dataSource="form.business.business_activities"> -->
          <!-- <template slot="name" slot-scope="name">{{name.first}} {{name.last}}</template> -->
          <!-- </a-table> -->
          <a-col :span="8" style="margin-top: -15px">
            <p class="inset">{{form.business.business_activities[i].line_business}}</p>
          </a-col>
          <a-col :span="8" style="margin-top: -15px">
            <p class="inset">{{form.business.business_activities[i].capital}}</p>
          </a-col>
          <a-col :span="8" style="margin-top: -15px">
            <p class="inset">{{form.business.business_activities[i].receipts}}</p>
          </a-col>
        </a-row>

        <!-- <a-col :span="12" style="margin-top: -25px">
            <a-form-item
              label="business_activities"
              :label-col="{ span: 8 }"
              :wrapper-col="{ span: 16 }"
            >
              <p>{{form.business.business_activities}}</p>
            </a-form-item>
        </a-col>-->
        <a-row>
          <!-- payment -->
          <a-col :span="24" style="margin-top: -15px">
            <p class="inset">
              Mode of Payment:
              <a-radio-group v-model="form.business.payment.mode" disabled="true">
                <a-radio :value="1">Annual/Full</a-radio>
                <a-radio :value="2">Quarterly</a-radio>
              </a-radio-group>No. of Quarters
              <u>{{form.business.payment.qrtly}}</u>
            </p>
            <!-- <a-form-item label="payment mode" :label-col="{ span: 8 }" :wrapper-col="{ span: 16 }">
              <p>{{form.business.payment.mode}}</p>
            </a-form-item>-->
          </a-col>
          <!-- <a-col :span="12" style="margin-top: -15px">
            <p class="inset">E-mail Address: {{form.business.rented.lessor_email}}</p>
            <a-form-item label="payment qrtly" :label-col="{ span: 8 }" :wrapper-col="{ span: 16 }">
              <p>{{form.business.payment.qrtly}}</p>
            </a-form-item>
          </a-col>-->
        </a-row>
        <a-row>
          <div align="right">
            <a-button>
              <a-icon type="download" />Download
            </a-button>
          </div>
        </a-row>
        <!-- <a-row> -->
        <!-- documents -->
        <!-- <a-col :span="12">
            <a-form-item
              label="uploaded documents"
              :label-col="{ span: 8 }"
              :wrapper-col="{ span: 16 }"
            >
              <p>{{form.documents}}</p>
            </a-form-item>
        </a-col>-->

        <!-- <a-col :span="12">
            <description-item title="">{{}}</description-item>
        </a-col>-->
        <!-- </a-row> -->
      </a-card>
      <a-card style="textAlign:'center'" v-show="current =='insurance'">
        <div align="center">
          <a-card hoverable style="width: 300px">
            <img
              v-if="form.business_insurance.provider == 'Malayan'"
              alt="example"
              src="https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcToEd_HUEVcw8aW1xYzakaludSmpdQyREP_JAxx5KFsRXqxQj8D"
              slot="cover"
            />
            <img
              v-if="form.business_insurance.provider == 'AIG'"
              alt="example"
              src="https://upload.wikimedia.org/wikipedia/commons/thumb/b/b3/AIG_logo.svg/1200px-AIG_logo.svg.png"
              slot="cover"
            />
            <img
              v-if="form.business_insurance.provider == 'AXA Philippines'"
              alt="example"
              src="https://pbs.twimg.com/profile_images/1039861366918508544/AYFe5Ooj_400x400.jpg"
              slot="cover"
            />
            <img
              v-if="form.business_insurance.provider == 'MAPRE Philippines'"
              alt="example"
              src="https://www.mapfre.com.ph/insurance-ph/images/1200x630-logo-mapfre_tcm844-83355.jpg"
              slot="cover"
            />
            <div align="center">
              <h3>{{form.business_insurance.provider}}</h3>
            </div>

            <a-card-grid style="width:50%;textAlign:'center'">Fee:</a-card-grid>
            <a-card-grid style="width:50%;textAlign:'center'">₱{{form.business_insurance.app_fee}}</a-card-grid>
            <a-card-grid style="width:50%;textAlign:'center'">LRF:</a-card-grid>
            <a-card-grid style="width:50%;textAlign:'center'">₱{{form.business_insurance.lrf}}</a-card-grid>
            <a-card-grid style="width:50%;textAlign:'center'">Interest:</a-card-grid>
            <a-card-grid style="width:50%;textAlign:'center'">₱{{form.business_insurance.interest}}</a-card-grid>
            <a-card-grid style="width:50%;textAlign:'center'">Surcharge:</a-card-grid>
            <a-card-grid style="width:50%;textAlign:'center'">₱{{form.business_insurance.surcharge}}</a-card-grid>
            <a-card-grid style="width:50%;textAlign:'center'">Total:</a-card-grid>
            <a-card-grid style="width:50%;textAlign:'center'">₱{{form.business_insurance.total}}</a-card-grid>
          </a-card>
        </div>

        <!-- business insurance
        <a-col :span="12">
          <a-form-item
            label="business insurance provider"
            :label-col="{ span: 8 }"
            :wrapper-col="{ span: 16 }"
          >
            <p>{{form.business_insurance.provider}}</p>
          </a-form-item>
        </a-col>
        <a-col :span="12">
          <a-form-item
            label="business insurance app fee"
            :label-col="{ span: 8 }"
            :wrapper-col="{ span: 16 }"
          >
            <p>{{form.business_insurance.app_fee}}</p>
          </a-form-item>
        </a-col>
        <a-col :span="12">
          <a-form-item
            label="business insurance lrf"
            :label-col="{ span: 8 }"
            :wrapper-col="{ span: 16 }"
          >
            <p>{{form.business_insurance.lrf}}</p>
          </a-form-item>
        </a-col>
        <a-col :span="12">
          <a-form-item
            label="business insurance interest"
            :label-col="{ span: 8 }"
            :wrapper-col="{ span: 16 }"
          >
            <p>{{form.business_insurance.interest}}</p>
          </a-form-item>
        </a-col>
        <a-col :span="12">
          <a-form-item
            label="business insurance surcharge"
            :label-col="{ span: 8 }"
            :wrapper-col="{ span: 16 }"
          >
            <p>{{form.business_insurance.surcharge}}</p>
          </a-form-item>
        </a-col>
        <a-col :span="12">
          <a-form-item
            label="business insurance total"
            :label-col="{ span: 8 }"
            :wrapper-col="{ span: 16 }"
          >
            <p>{{form.business_insurance.total}}</p>
          </a-form-item>
        </a-col>-->
      </a-card>
      <a-card style="textAlign:'center'" v-show="current =='payment'">
        <div align="center">
          <a-card title="Payment Details" style="width:50%">
            <a-card-grid style="width:50%;textAlign:'center'">Permit Type:</a-card-grid>
            <a-card-grid style="width:50%;textAlign:'center'">{{form.payment_info.desc}}</a-card-grid>
            <a-card-grid style="width:50%;textAlign:'center'">Fee:</a-card-grid>
            <a-card-grid style="width:50%;textAlign:'center'">{{form.payment_info.amount}}</a-card-grid>
            <a-card-grid style="width:50%;textAlign:'center'">Payment Method:</a-card-grid>
            <a-card-grid style="width:50%;textAlign:'center'">{{form.payment_info.method}}</a-card-grid>
            <a-card-grid style="width:50%;textAlign:'center'">Name:</a-card-grid>
            <a-card-grid style="width:50%;textAlign:'center'">{{form.billing_info.name}}</a-card-grid>
            <a-card-grid
              style="width:50%;textAlign:'center'"
              v-if="form.billing_info.credit_card != null"
            >Credit Card Number:</a-card-grid>
            <a-card-grid
              style="width:50%;textAlign:'center'"
              v-if="form.billing_info.credit_card
            !=null"
            >{{form.billing_info.credit_card}}</a-card-grid>
            <a-card-grid style="width:50%;textAlign:'center'">Email:</a-card-grid>
            <a-card-grid style="width:50%;textAlign:'center'">{{form.billing_info.email}}</a-card-grid>
            <a-card-grid style="width:50%;textAlign:'center'">Contact:</a-card-grid>
            <a-card-grid style="width:50%;textAlign:'center'">{{form.billing_info.contact}}</a-card-grid>
            <a-card-grid style="width:50%;textAlign:'center'">
              <p>Status:</p>
            </a-card-grid>
            <a-card-grid style="width:50%;textAlign:'center'">
              <p v-if="form.progress.current_task != 'Payment'" text-color="success">Paid</p>
              <p v-else text-color="error">UnPaid</p>
            </a-card-grid>
          </a-card>
        </div>
        <!-- payment info -->
        <!-- <a-col :span="12">
          <a-form-item label="description" :label-col="{ span: 8 }" :wrapper-col="{ span: 16 }">
            <p>{{form.payment_info.desc}}</p>
          </a-form-item>
        </a-col>
        <a-col :span="12">
          <a-form-item label="amount" :label-col="{ span: 8 }" :wrapper-col="{ span: 16 }">
            <p>{{form.payment_info.amount}}</p>
          </a-form-item>
        </a-col>
        <a-col :span="12">
          <a-form-item label="method" :label-col="{ span: 8 }" :wrapper-col="{ span: 16 }">
            <p>{{form.payment_info.method}}</p>
          </a-form-item>
        </a-col>
        <!-- billing info-->
        <!-- <a-col :span="12">
          <a-form-item label="name" :label-col="{ span: 8 }" :wrapper-col="{ span: 16 }">
            <p>{{form.billing_info.name}}</p>
          </a-form-item>
        </a-col>
        <a-col :span="12">
          <a-form-item label="email" :label-col="{ span: 8 }" :wrapper-col="{ span: 16 }">
            <p>{{form.billing_info.email}}</p>
          </a-form-item>
        </a-col>
        <a-col :span="12">
          <a-form-item label="contact" :label-col="{ span: 8 }" :wrapper-col="{ span: 16 }">
            <p>{{form.billing_info.contact}}</p>
          </a-form-item>
        </a-col>-->
        <!-- progress-->
        <!-- <a-col :span="12">
          <a-form-item label="status" :label-col="{ span: 8 }" :wrapper-col="{ span: 16 }">
            <p>{{form.progress.status}}</p>
          </a-form-item>
        </a-col>
        <a-col :span="12">
          <a-form-item label="current_task" :label-col="{ span: 8 }" :wrapper-col="{ span: 16 }">
            <p>{{form.progress.current_task}}</p>
          </a-form-item>
        </a-col>-->
      </a-card>
    </a-drawer>
  </a-card>
</template>

<script>
import { stringify } from "querystring";
import axios from "axios";

export default {
  data() {
    return {
      current: ["permit"],
      form: {
        application: {
          permit_type: "",
          app_type: null,
          reference_no: null,
          pbr_date: null,
          lgu_date: null,
          registration_no: null
        },
        business: {
          ownership: null,
          tin: null,
          sss: null,
          business_name: "",
          contact: null,
          email: "",
          business_address: "",
          // AMO - Applicat/Manager/Owner
          amo: {
            name: "",
            address: "",
            contact: null,
            email: ""
          },
          business_area: "",
          owner_no: null,
          employees_no: {
            professional: null,
            non_professional: null
          },
          business_type: null,
          rented: {
            lessor: "",
            monthly_rental: null,
            lessor_address: "",
            lessor_conatct: null,
            lessor_email: ""
          },
          property_pin: {
            land: null,
            building: null,
            machinery: null
          },
          business_activities: [],
          payment: {
            mode: null,
            qrtly: null
          }
        },
        documents: [],
        business_insurance: {
          provider: "",
          app_fee: 0,
          lrf: 0,
          interest: 0,
          surcharge: 0,
          total: 0
        },
        payment_info: {
          desc: "Business Clearance",
          amount: 1500,
          method: "Over the Counter"
        },
        billing_info: {
          credit_number: null,
          name: "",
          email: "",
          contact: null
        },
        progress: {
          status: "",
          current_task: "",
          previous_task: ""
        }
      },
      columns: [
        {
          title: "Line of Business",
          dataIndex: "line_business",
          width: "30%",
          scopedSlots: { customRender: "line_business" }
        },
        {
          title: "Capitalization",
          dataIndex: "capital",
          scopedSlots: { customRender: "capital" }
        },
        {
          title: "Gross Sales/Receipts",
          dataIndex: "receipts",
          scopedSlots: { customRender: "receipts" }
        }
      ],
      transac: [
        // {
        //   ref_no: 1,
        //   permit: "Business Permit",
        //   type: "Initial",
        //   status: "On Process",
        //   current_task: "Payment",
        //   pbr_date: "09/05/2019",
        //   lgu_date: "09/05/2019",
        //   reg_no: "01",
        //   ownership: "owned",
        //   tin: 123456789,
        //   sss: 123456789,
        //   business_name: "negosyo",
        //   contact_num: 321,
        //   email: "email@email.email",
        //   business_address: "location"
        // },
        // {
        //   reference_no: 2,
        //   permit: "Business Permit",
        //   type: "Initial",s
        //   status: "On Process",
        //   current_task: "Payment",
        //   pbr_date: "09/05/2019",
        //   lgu_date: "09/05/2019",
        //   reg_no: "01",
        //   ownership: "owned",
        //   tin: 123456789,
        //   sss: 123456789,
        //   business_name: "negosyo",
        //   contact_num: 321,
        //   email: "email@email.email",
        //   business_address: "location"
        // }
      ],
      cols: [
        {
          title: "Permit",
          dataIndex: "application.permit_type"
        },
        {
          title: "Type",
          dataIndex: "application.app_type",
          scopedSlots: { customRender: "application.app_type" }
        },
        {
          title: "Status",
          dataIndex: "progress.status"
        },
        {
          title: "Current Task",
          dataIndex: "progress.current_task"
        },
        {
          title: "Action",
          dataIndex: "action",
          scopedSlots: { customRender: "action" }
        }
      ],
      draw_show: false
    };
  },
  created() {
    console.log();
    axios.get("permit/apply").then(data => {
      console.log("get all saved data: " + JSON.stringify(data));
      data.data.forEach(element => {
        this.transac.push(element);
      });
    });
  },
  methods: {
    view_data(data) {
      this.form = data;
      console.log("viewed item: " + JSON.stringify(data));
      this.draw_show = true;
    },
    onClose() {
      this.draw_show = false;
    }
  }
};
</script>
<style>
p.dotted {
  border-style: dotted;
}
p.dashed {
  border-style: dashed;
}
p.solid {
  border-style: solid;
}
p.double {
  border-style: double;
}
p.groove {
  border-style: groove;
}
p.ridge {
  border-style: ridge;
}
p.inset {
  border-style: inset;
}
p.outset {
  border-style: outset;
}
p.none {
  border-style: none;
}
p.hidden {
  border-style: hidden;
}
p.mix {
  border-style: dotted dashed solid double;
}
</style>