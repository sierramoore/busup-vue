<template>
  <v-data-table
    :headers="headers"
    :items="costCenterEntries"
    :items-per-page="5"
    class="tableContainer"
  >
      <template v-slot:top>
      <v-toolbar
        flat
      >
        <v-toolbar-title>Cost Center</v-toolbar-title>
        <v-divider
          class="mx-4"
          inset
          vertical
        ></v-divider>
        <v-spacer></v-spacer>
        <v-dialog
          v-model="dialog"
          max-width="500px"
        >
          <template v-slot:activator="{ on, attrs }">
            <v-btn
              color="primary"
              dark
              class="mb-2"
              v-bind="attrs"
              v-on="on"
            >
              New Item
            </v-btn>
          </template>
          <v-card>
            <v-card-title>
              <span class="headline">New Entry</span>
            </v-card-title>

            <v-card-text>
              <v-container>
                <v-row>
                  <v-col
                    cols="12"
                    sm="6"
                    md="4"
                  >
                    <v-text-field
                      v-model="editedEntry.id"
                      label="ID"
                    ></v-text-field>
                  </v-col>
                  <v-col
                    cols="12"
                    sm="6"
                    md="4"
                  >
                    <v-text-field
                      v-model="editedEntry.name"
                      label="Name"
                    ></v-text-field>
                  </v-col>
                  <v-col
                    cols="12"
                    sm="6"
                    md="4"
                  >
                    <v-text-field
                      v-model="editedEntry.company_id"
                      label="Company ID"
                    ></v-text-field>
                  </v-col>
                </v-row>
              </v-container>
            </v-card-text>

            <v-card-actions>
              <v-spacer></v-spacer>
              <v-btn
                color="blue darken-1"
                text
                @click="close"
              >
                Cancel
              </v-btn>
              <v-btn
                color="blue darken-1"
                text
                @click="save"
              >
                Save
              </v-btn>
            </v-card-actions>
          </v-card>
        </v-dialog>
      </v-toolbar>
    </template>
  </v-data-table>
</template>


<script>
// import axios from "axios";

export default {
  name: "CostCenter",

  data() {
    return {
      accessToken:
        "eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsImp0aSI6IjQ3NTVjMDdjMDQ1MzRjYTU4ZTcwNGEzYjhjYzBiMTQ5ZGVhMWJiMDdmYzMxN2Q0NTNjNDVhNTdmMzE3M2Y1OWIyZmUxNjk1ZmU0YzgzM2IyIn0.eyJhdWQiOiIyIiwianRpIjoiNDc1NWMwN2MwNDUzNGNhNThlNzA0YTNiOGNjMGIxNDlkZWExYmIwN2ZjMzE3ZDQ1M2M0NWE1N2YzMTczZjU5YjJmZTE2OTVmZTRjODMzYjIiLCJpYXQiOjE2MTcwMDY0MjUsIm5iZiI6MTYxNzAwNjQyNSwiZXhwIjoxNjE4MzAyNDI0LCJzdWIiOiIiLCJzY29wZXMiOltdfQ.S_nFnQxWafk17YsaEMQCFxogkboaUu8q59WMfPSlBUxMZWSaeEV7J1MoK19ONOukKwn93sutQwAewJv_jNLeqopVU0de-iD2tmsGp0T-CyCDLjA0ZZnQ8YGNVXiXlwTYwHhOogKdM9ozqWtsvQcwXVLyzpNdIsvuxNCoXrKt_9rNy50nqTnMKaVCVkOtmfrKPxfXbXRQ-4UL9rdUkd6QTH9Y6_N9VeEs9LtGL30G6dVmgutLnW4f41eXFT37157wU5TAU4qh-YTxFd_AYH9njN-SPDfCA3B7BPaBDzaB7BOe4sft7stMt2uNhZpt-U_UdZIPuXszhH_D4u5dvHkp5RDGS4QIFsI-UXbCslK9f8L-A9ig0LuK98uERdkTUuI9DmqxjccitEekk-wlnViWbhE9MsMyIiG77CfCCNWXPnm-oPW-CZnuQTKU4yFdMxDQIFCRDUQaLgMvkx7hKtQOHBURZYDlnq0dOeoC5tvlySJqw3oRRXBrHShAtNPaQM6aGq4CrY7ztYHCqtCD6NSuOy35XOzUAUm_5ZeW5Tp0C-QiA8SH9O_knhPu1zhWFFCLWUQn7dFrOHRP34DBMGrEOYnyjKkRrLWhZYa-71SFrJFZ25LeAvAbVz5XwZNmPoIm7sAu0NIqKg5LjZCER0XM-T7L71CFGLNCjQ2_LdzLshs",
      headers: [
        { text: "ID", align: "start", sortable: false, value: "id" },
        { text: "Name", sortable: false, value: "name" },
        { text: "Company ID", sortable: false, value: "company_id" }
      ],
      costCenterEntries: [
        {
          id: "1",
          name: "test qa5",
          company_id: 29
        },
        {
          id: "2",
          name: "test 2",
          company_id: 29
        },
        {
          id: "3",
          name: "test Ed",
          company_id: 29
        },
        {
          id: "4",
          name: "test 4",
          company_id: 29
        },
        {
          id: "5",
          name: "test 47",
          company_id: 29
        }
      ],
      editedEntryIndex: -1,
      editedEntry: {
        id: "",
        name: "",
        company_id: ""
      },
      defaultEntry: {
        id: 0,
        name: "Joe",
        company_id: "00"
      },
      dialog: false,
      watch: {
        dialog(val) {
          val || this.close();
        }
      }
    };
    // mounted() {
    // axios
    //   .get("https://api.qa5.busup.org/app/dashboard/api/v1/cost_centers", {
    //     headers: {
    //       Authorization: `Bearer ${this.accessToken}`
    //     }
    //   })
    //   .then(response => {
    //     this.costCenterEntries = response.data.data.table;
    //   })
    //   .catch(err => console.log(err));
    // }
  },
  methods: {
    save() {
      if (this.editedEntryIndex > -1) {
        Object.assign(
          this.costCenterEntries[this.editedEntryIndex],
          this.editedEntry
        );
      } else {
        this.costCenterEntries.push(this.editedEntry);
      }
      this.close();
    },
    close() {
      this.dialog = false;
      this.$nextTick(() => {
        this.editedEntry = Object.assign({}, this.defaultEntry);
        this.editedEntryIndex = -1;
      });
    }
  }
};
</script>

<style scoped>
.v-data-table {
  max-width: 600px;
  margin: 50px auto;
}
</style>
