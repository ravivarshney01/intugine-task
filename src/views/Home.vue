<template>
  <div class="home">
    <v-container fluid>
      <v-item-group class="mb-6" mandatory>
        <v-row align="center" justify="center">
          <v-item class="ma-3" v-slot:default="{ active, toggle }">
            <v-card
              :color="active ? 'rgb(49, 107, 253)' : 'rgb(213, 222, 254)'"
              class="d-flex align-start flex-column pa-2"
              @click="
                toggle();
                search = 'Delivered';
              "
              height="100"
              width="100"
            >
              <span
                class="mb-auto "
                :style="
                  !active
                    ? 'color: rgb(49, 107, 253); font-size: 15px '
                    : 'color: rgb(244,246,252); font-size: 15px '
                "
              >
                DEL
              </span>
              <span
                :style="
                  !active
                    ? 'color: rgb(49, 107, 253); font-size: 36px '
                    : 'color: rgb(244,246,252); font-size: 36px '
                "
                >{{ del }}</span
              >
            </v-card>
          </v-item>
          <v-item class="ma-3" v-slot:default="{ active, toggle }">
            <v-card
              :color="active ? 'rgb(49, 107, 253)' : 'rgb(213, 222, 254)'"
              class="d-flex align-start flex-column pa-2"
              @click="
                toggle();
                search = 'In Transit';
              "
              height="100"
              width="100"
            >
              <span
                class="mb-auto "
                :style="
                  !active
                    ? 'color: rgb(49, 107, 253); font-size: 15px '
                    : 'color: rgb(244,246,252); font-size: 15px '
                "
              >
                INT
              </span>
              <span
                :style="
                  !active
                    ? 'color: rgb(49, 107, 253); font-size: 36px '
                    : 'color: rgb(244,246,252); font-size: 36px '
                "
                >{{ int }}</span
              >
            </v-card>
          </v-item>
          <v-item class="ma-3" v-slot:default="{ active, toggle }">
            <v-card
              :color="active ? 'rgb(49, 107, 253)' : 'rgb(213, 222, 254)'"
              class="d-flex align-start flex-column pa-2"
              @click="
                toggle();
                search = 'Out for Delivery';
              "
              height="100"
              width="100"
            >
              <span
                class="mb-auto "
                :style="
                  !active
                    ? 'color: rgb(49, 107, 253); font-size: 15px '
                    : 'color: rgb(244,246,252); font-size: 15px '
                "
              >
                OOD
              </span>
              <span
                :style="
                  !active
                    ? 'color: rgb(49, 107, 253); font-size: 36px '
                    : 'color: rgb(244,246,252); font-size: 36px '
                "
                >{{ ood }}</span
              >
            </v-card>
          </v-item>
          <v-item class="ma-3" v-slot:default="{ active, toggle }">
            <v-card
              :color="active ? 'rgb(49, 107, 253)' : 'rgb(213, 222, 254)'"
              class="d-flex align-start flex-column pa-2"
              @click="
                toggle();
                search = 'Undelivered';
              "
              height="100"
              width="100"
            >
              <span
                class="mb-auto "
                :style="
                  !active
                    ? 'color: rgb(49, 107, 253); font-size: 15px '
                    : 'color: rgb(244,246,252); font-size: 15px '
                "
              >
                UND
              </span>
              <span
                :style="
                  !active
                    ? 'color: rgb(49, 107, 253); font-size: 36px '
                    : 'color: rgb(244,246,252); font-size: 36px '
                "
                >{{ und }}</span
              >
            </v-card>
          </v-item>
        </v-row>
      </v-item-group>
      <v-row align="center" justify="center">
        <v-col xs="6" class="ma-2" style="border: 1px solid rgb(213,222,254)">
          <v-timeline dense>
            <v-timeline-item color="rgb(213,222,254)" fill-dot>
              <template v-slot:icon>
                <v-avatar width="15px">
                  <img src="../assets/destination.svg" />
                </v-avatar>
              </template>
            </v-timeline-item>

            <TimelineItem
              v-for="(item, k) in timeline"
              :key="k"
              :item="item"
            ></TimelineItem>

            <v-timeline-item color="rgb(213,222,254)" fill-dot>
              <template v-slot:icon>
                <v-avatar width="15px">
                  <img src="../assets/warehouse.svg" />
                </v-avatar>
              </template>
            </v-timeline-item>
          </v-timeline>
        </v-col>
        <v-col
          xs="6"
          class="pa-0 pr-5"
          style="border: 1px solid rgb(213,222,254)"
        >
          <v-data-table
            :headers="headers"
            @click:row="select"
            :items="columns"
            :search="search"
            :custom-filter="filterOnlyCapsText"
            disable-pagination
            fixed-header
            hide-default-footer
            height="500"
          >
            <template v-slot:item.status="{ item }">
              <span
                :style="
                  item.status == 'Delivered' ? 'color:green' : 'color: black'
                "
              >
                {{ item.status }}
              </span>
            </template>
          </v-data-table>
        </v-col>
      </v-row>
    </v-container>
  </div>
</template>

<script>
// @ is an alias to /src
import axios from "axios";
import moment from "moment";
import TimelineItem from "@/components/TimelineItem";

export default {
  name: "Home",
  components: {
    TimelineItem
  },
  data() {
    return {
      del: 0,
      ood: 0,
      und: 0,
      int: 0,
      search: "Delivered",
      timeline: 0,
      columns: [],
      headers: [
        { text: "AWB Number", value: "awb" },
        { text: "Transporter", value: "trans", sortable: false },
        { text: "Source", value: "source", sortable: false },
        { text: "Destination", value: "dest", sortable: false },
        { text: "Brand", value: "brand", sortable: false },
        { text: "Start Date", value: "sdate", sortable: false },
        { text: "EDT", value: "edt", sortable: false },
        {
          text: "Status",
          value: "status",
          sortable: false
        }
      ]
    };
  },
  created() {
    axios.defaults.headers.common["Authorization"] = "Bearer tTU3gFVUdP";
    axios
      .post(
        "https://93870v1pgk.execute-api.ap-south-1.amazonaws.com/latest/shipments/ravi",
        {
          email: "ravivarshney49@gmail.com"
        }
      )
      .then(res => {
        var d;
        this.timeline = res.data.data[0].scan;
        res.data.data.forEach(r => {
          d = {
            awb: "#" + r.awbno,
            trans: r.carrier,
            source: this.capitalize(r.from),
            dest: this.capitalize(r.to),
            brand: r.carrier,
            sdate: moment(r.pickup_date).format("DD/MM/YYYY"),
            edt: moment(r.extra_fields.expected_delivery_date).format(
              "DD/MM/YYYY"
            ),
            status: r.current_status,
            code: r.current_status_code,
            scan: r.scan
          };
          if (r.current_status_code == "DEL") {
            this.del++;
          } else if (r.current_status_code == "INT") {
            this.int++;
          } else if (r.current_status_code == "OOD") {
            this.ood++;
          } else if (r.current_status_code == "UND") {
            this.und++;
          }
          this.columns.push(d);
        });
      })
      .catch(err => {
        console.log(err);
      });
  },
  methods: {
    capitalize(string) {
      return string.charAt(0).toUpperCase() + string.toLowerCase().slice(1);
    },
    filterOnlyCapsText(value, search, item) {
      return value.toString().indexOf(search) !== -1;
    },
    select(r) {
      this.timeline = r.scan;
    }
  }
};
</script>
<style>
.v-data-table-header__icon {
  display: none !important;
}

tr {
  border: 1px solid rgb(239, 242, 254);
}

.v-data-table th {
  height: 30px !important;
}
::-webkit-scrollbar {
  width: 10px;
}

/* Track */
::-webkit-scrollbar-track {
  box-shadow: inset 0 0 5px rgb(213, 222, 254);
  border-radius: 5px;
  background: rgb(213, 222, 254);
}

/* Handle */
::-webkit-scrollbar-thumb {
  background: rgb(61, 116, 252);
  border-radius: 10px;
}

/* Handle on hover */
::-webkit-scrollbar-thumb:hover {
  background: rgb(49, 107, 253);
}
</style>
