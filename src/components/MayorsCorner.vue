<template>
  <a-row type="flex" :gutter="16">
    <a-col :span="24">
      <template v-if="loading">
        <a-card>
          <div v-for="i in 4" :key="i">
            <a-skeleton active avatar :paragraph="{rows: 4}" />
            <a-divider></a-divider>
          </div>
        </a-card>
      </template>

      <template v-else>
        <a-card style="margin-bottom: 2vh">
          <a-comment>
            <template slot="actions">
              <span>
                <a-tooltip title="Like">
                  <a-icon
                    type="like"
                    :theme="action === 'liked' ? 'filled' : 'outlined'"
                    @click="like"
                  />
                </a-tooltip>
                <span style="padding-left: '8px';cursor: 'auto'">{{likes}}</span>
              </span>
              <span>
                <a-tooltip title="Dislike">
                  <a-icon
                    type="dislike"
                    :theme="action === 'disliked' ? 'filled' : 'outlined'"
                    @click="dislike"
                  />
                </a-tooltip>
                <span style="padding-left: '8px';cursor: 'auto'">{{dislikes}}</span>
              </span>
            </template>
            <a slot="author">Mayor Orlan Calayag</a>
            <a-avatar
              src="https://i.postimg.cc/kgS0jvKG/67173199-717906838645209-9201731590730809344-n.jpg"
              alt="Mayor Orlan photo"
              slot="avatar"
            />
            <span slot="content">
              Pormal na pong inactivate ang ating Incident Command System para sa 2nd District Congressional Athletic Meet 2019 na gaganapin sa Dolores ngayong Setyembre 18-21.Nagbigay po ng kanyang mensahe ang ating mahal na Mayor Kgg. ORLAN A. CALAYAG sa lahat ng dumalo sa Solidarity Meeting upang personal silang tanggapin sa Bayan ng Dolores.
              <br />
              <br />Nagbigay din po ng mga safety measures at tips ang Incident Management Team para sa mas magandang takbo ng operasyon ng event na ito. Binubuo po ito ng DepEd, Office of the Mayor, Tourism, Budget, Assessor, PNP, MDRRMO, MENRO at BFP.
              <br />
              <br />Maligayang pagdating sa Bayan ng Dolores!
              <br />
              <b>#UNLADDOLORES</b>
              <a-row type="flex" justify="left" :gutter="8">
                <a-col :span="8" v-for="i in 3" :key="i">
                  <img :src="`https://picsum.photos/300?random=${indx}${i}`" width="200vw" />
                </a-col>
              </a-row>
            </span>
            <a-tooltip slot="datetime" :title="moment().format('YYYY-MM-DD HH:mm:ss')">
              <span>{{moment().fromNow()}}</span>
            </a-tooltip>
          </a-comment>
        </a-card>

        <a-card style="margin-bottom: 2vh">
          <a-comment>
            <template slot="actions">
              <span>
                <a-tooltip title="Like">
                  <a-icon
                    type="like"
                    :theme="action === 'liked' ? 'filled' : 'outlined'"
                    @click="like"
                  />
                </a-tooltip>
                <span style="padding-left: '8px';cursor: 'auto'">{{likes}}</span>
              </span>
              <span>
                <a-tooltip title="Dislike">
                  <a-icon
                    type="dislike"
                    :theme="action === 'disliked' ? 'filled' : 'outlined'"
                    @click="dislike"
                  />
                </a-tooltip>
                <span style="padding-left: '8px';cursor: 'auto'">{{dislikes}}</span>
              </span>
            </template>
            <a slot="author">Mayor Orlan Calayag</a>
            <a-avatar
              src="https://i.postimg.cc/kgS0jvKG/67173199-717906838645209-9201731590730809344-n.jpg"
              alt="Mayor Orlan photo"
              slot="avatar"
            />
            <span slot="content">
              ICS Fully Activated. Our objectives are:
              <br />Ensure safety of athletes, delegates, officials, organizers and guests at all times
              <br />Maintain peace and order in all areas of the Congressional Athletic Meet 2019 at all times.
              <br />
              <br />Event: Congressman's Night
              <br />Venue: Dolores Events Center
              <br />Date/Time: 17 Sep 2019 1800H - 18 Sep 2019 0001H
              <br />
              <br />Thank you everyone for cooperating. Mission accomplished! Zero incident on Day Zero!
              <br />
              <br />Thank you Hon. MAYOR ORLAN A. CALAYAG for being resilient in Crises and Disaster Risk Reduction Management.
              <br />
              <br />#UNLADDOLORES
              <br />#ICS
              <br />#CongressionalAthleticMeet2019
              <a-row type="flex" justify="left" :gutter="8">
                <a-col :span="8" v-for="i in 3" :key="i">
                  <img :src="`https://picsum.photos/300?random=${indx}${i}`" width="200vw" />
                </a-col>
              </a-row>
            </span>
            <a-tooltip slot="datetime" :title="moment().format('YYYY-MM-DD HH:mm:ss')">
              <span>{{moment().fromNow()}}</span>
            </a-tooltip>
          </a-comment>
        </a-card>

        <a-card style="margin-bottom: 2vh">
          <a-comment>
            <template slot="actions">
              <span>
                <a-tooltip title="Like">
                  <a-icon
                    type="like"
                    :theme="action === 'liked' ? 'filled' : 'outlined'"
                    @click="like"
                  />
                </a-tooltip>
                <span style="padding-left: '8px';cursor: 'auto'">{{likes}}</span>
              </span>
              <span>
                <a-tooltip title="Dislike">
                  <a-icon
                    type="dislike"
                    :theme="action === 'disliked' ? 'filled' : 'outlined'"
                    @click="dislike"
                  />
                </a-tooltip>
                <span style="padding-left: '8px';cursor: 'auto'">{{dislikes}}</span>
              </span>
            </template>
            <a slot="author">Mayor Orlan Calayag</a>
            <a-avatar
              src="https://i.postimg.cc/kgS0jvKG/67173199-717906838645209-9201731590730809344-n.jpg"
              alt="Mayor Orlan photo"
              slot="avatar"
            />
            <span slot="content">
              Ang pagiging handa ay sagot sa anumang sakuna o kalamidad!
              <br />Maging alerto. Maging mapagmatyag. Maging handa!
              <br />#UNLADDOLORES
              <br />
              <br />Dolores Tourism: Faith and Wellness Destination
              <a-row type="flex" justify="left" :gutter="8">
                <a-col :span="8" v-for="i in 3" :key="i">
                  <img :src="`https://picsum.photos/300?random=${indx}${i}`" width="200vw" />
                </a-col>
              </a-row>
            </span>
            <a-tooltip slot="datetime" :title="moment().format('YYYY-MM-DD HH:mm:ss')">
              <span>{{moment().fromNow()}}</span>
            </a-tooltip>
          </a-comment>
        </a-card>
      </template>
    </a-col>
  </a-row>
</template>

<script>
import moment from "moment";
export default {
  data() {
    return {
      subscribers: [],
      moment,
      likes: 30,
      dislikes: 0,
      action: null,
      loading: false
    };
  },
  created() {
    this.init();
  },
  methods: {
    init() {
      this.loading = true;
      this.$http
        .get("https://randomuser.me/api/?results=20")
        .then(results => {
          console.log("::::", JSON.stringify(results));
          this.subscribers = results.data.results;
          this.loading = false;
        })
        .catch(err => {
          console.log(err);
          this.loading = false;
          // this.$notification.error({
          // })
        });
    }
  }
};
</script>

<style>
.ant-skeleton-content .ant-skeleton-title {
  height: 9px;
}

.ant-skeleton-content .ant-skeleton-paragraph > li {
  height: 9px;
}
</style>
