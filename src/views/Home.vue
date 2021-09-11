<template>
  <div>
    <p class="mb-10 mx-auto mt-4 text--accent-4 text-center" width="344">List of calendars</p>
    <v-card
        v-for="(calendar, index) in calendars"
        :key="index"
        class="mx-auto mb-1"
        max-width="344"
        outlined
    >
      <v-list-item three-line>
        <v-list-item-content>
          <div class="text-overline mb-4">
            {{calendar.clientName}}
          </div>
          <v-list-item-title class="text-h5 mb-1">

          </v-list-item-title>
          <v-list-item-subtitle>{{ parseDate(calendar.date) }}</v-list-item-subtitle>
        </v-list-item-content>
      </v-list-item>

      <v-card-actions>
        <v-btn
            @click="openDialog(calendar)"
            outlined
            rounded
            text
        >
          Send reminder
        </v-btn>
      </v-card-actions>
    </v-card>

    <v-dialog v-model="dialog" width="500">
      <div>
        <v-card>
          <template slot="progress">
            <v-progress-linear
                color="deep-purple"
                height="10"
                indeterminate
            ></v-progress-linear>
          </template>

          <v-img
              height="250"
              src="https://www.cnppid.com/wp-content/uploads/2017/10/wateryearcalendar.jpg"
          ></v-img>

          <v-card-title>Set Reminder</v-card-title>

          <v-card-text>
            <div class="my-4 text-subtitle-1">
              {{calendar.clientName}}
            </div>

            <div>Choose when to send reminder email to this client.</div>
          </v-card-text>

          <v-divider class="mx-4"></v-divider>

          <v-card-title>Available options</v-card-title>

          <v-card-text>
            <v-chip-group
                v-model="selection"
                active-class="deep-purple accent-4 white--text"
                column
            >
              <v-chip>daily</v-chip>

              <v-chip>weekly</v-chip>

              <v-chip>monthly</v-chip>

              <v-chip>yearly</v-chip>
            </v-chip-group>
          </v-card-text>

          <v-card-text v-if="selection !== null">
            <v-select
                class="d-inline"
                style="width: 100px;"
                v-model="sendEach"
                :items="[1,2,3,4,5,6,7,8,9]"
                :label="'Send each x ' + selectionType"
            ></v-select>
          </v-card-text>

          <v-card-title>Send reminder emails until:</v-card-title>

          <v-card-text>
            <v-menu
                ref="showDate"
                v-model="showDate"
                :close-on-content-click="false"
                :return-value.sync="sendUntil"
                transition="scale-transition"
                offset-y
                min-width="auto"
            >
              <template v-slot:activator="{ on, attrs }">
                <v-text-field
                    v-model="sendUntil"
                    label="Picker in menu"
                    prepend-icon="mdi-calendar"
                    readonly
                    v-bind="attrs"
                    v-on="on"
                ></v-text-field>
              </template>
              <v-date-picker
                  v-model="sendUntil"
                  no-title
                  scrollable
              >
                <v-spacer></v-spacer>
                <v-btn
                    text
                    color="primary"
                    @click="showDate = false"
                >
                  Cancel
                </v-btn>
                <v-btn
                    text
                    color="primary"
                    @click="$refs.showDate.save(sendUntil)"
                >
                  OK
                </v-btn>
              </v-date-picker>
            </v-menu>
          </v-card-text>

          <v-card-text v-if="showError">
            <p style="color: red;">Please fill in all the fields before sending the reminder.</p>
          </v-card-text>

          <v-card-actions>
            <v-btn
                color="deep-purple lighten-2"
                text
                @click="sendReminder"
            >
              Send reminder
            </v-btn>
          </v-card-actions>
        </v-card>
      </div>
    </v-dialog>
  </div>
</template>

<script>
  const axios = require('axios').default;

  export default {
    name: 'Home',

    components: {
    },

    data() {
      return {
        dialog: false,
        calendars: [
          {
            clientName: 'Angelina Jolie',
            date: new Date(),
          },
          {
            clientName: 'Angelina Jolie',
            date: new Date(),
          },
          {
            clientName: 'Angelina Jolie',
            date: new Date(),
          },
          {
            clientName: 'Angelina Jolie',
            date: new Date(),
          },
          {
            clientName: 'Angelina Jolie',
            date: new Date(),
          },
          {
            clientName: 'Angelina Jolie',
            date: new Date(),
          },
          {
            clientName: 'Angelina Jolie',
            date: new Date(),
          },
          {
            clientName: 'Angelina Jolie',
            date: new Date(),
          },
          {
            clientName: 'Angelina Jolie',
            date: new Date(),
          },
          {
            clientName: 'Angelina Jolie',
            date: new Date(),
          },
          {
            clientName: 'Angelina Jolie',
            date: new Date(),
          },
          {
            clientName: 'Angelina Jolie',
            date: new Date(),
          },
          {
            clientName: 'Angelina Jolie',
            date: new Date(),
          },
          {
            clientName: 'Angelina Jolie',
            date: new Date(),
          },
          {
            clientName: 'Angelina Jolie',
            date: new Date(),
          },
          {
            clientName: 'Angelina Jolie',
            date: new Date(),
          },
          {
            clientName: 'Angelina Jolie',
            date: new Date(),
          },
          {
            clientName: 'Angelina Jolie',
            date: new Date(),
          },
          {
            clientName: 'Angelina Jolie',
            date: new Date(),
          },
          {
            clientName: 'Angelina Jolie',
            date: new Date(),
          },
          {
            clientName: 'Angelina Jolie',
            date: new Date(),
          },
          {
            clientName: 'Angelina Jolie',
            date: new Date(),
          },
          {
            clientName: 'Angelina Jolie',
            date: new Date(),
          },
          {
            clientName: 'Angelina Jolie',
            date: new Date(),
          },
          {
            clientName: 'Angelina Jolie',
            date: new Date(),
          },
          {
            clientName: 'Angelina Jolie',
            date: new Date(),
          },
          {
            clientName: 'Angelina Jolie',
            date: new Date(),
          },
          {
            clientName: 'Angelina Jolie',
            date: new Date(),
          },
          {
            clientName: 'Angelina Jolie',
            date: new Date(),
          },
          {
            clientName: 'Angelina Jolie',
            date: new Date(),
          },
          {
            clientName: 'Angelina Jolie',
            date: new Date(),
          },
          {
            clientName: 'Angelina Jolie',
            date: new Date(),
          },
          {
            clientName: 'Angelina Jolie',
            date: new Date(),
          },
          {
            clientName: 'Angelina Jolie',
            date: new Date(),
          },
          {
            clientName: 'Angelina Jolie',
            date: new Date(),
          },
          {
            clientName: 'Angelina Jolie',
            date: new Date(),
          },
          {
            clientName: 'Angelina Jolie',
            date: new Date(),
          },
          {
            clientName: 'Angelina Jolie',
            date: new Date(),
          },
          {
            clientName: 'Angelina Jolie',
            date: new Date(),
          },
          {
            clientName: 'Angelina Jolie',
            date: new Date(),
          },
          {
            clientName: 'Angelina Jolie',
            date: new Date(),
          },
          {
            clientName: 'Angelina Jolie',
            date: new Date(),
          },
          {
            clientName: 'Angelina Jolie',
            date: new Date(),
          },
          {
            clientName: 'Angelina Jolie',
            date: new Date(),
          },
          {
            clientName: 'Angelina Jolie',
            date: new Date(),
          },
          {
            clientName: 'Angelina Jolie',
            date: new Date(),
          },
          {
            clientName: 'Angelina Jolie',
            date: new Date(),
          },
          {
            clientName: 'Angelina Jolie',
            date: new Date(),
          },
          {
            clientName: 'Angelina Jolie',
            date: new Date(),
          },
          {
            clientName: 'Angelina Jolie',
            date: new Date(),
          },
          {
            clientName: 'Angelina Jolie',
            date: new Date(),
          },
          {
            clientName: 'Angelina Jolie',
            date: new Date(),
          },
          {
            clientName: 'Angelina Jolie',
            date: new Date(),
          },
          {
            clientName: 'Angelina Jolie',
            date: new Date(),
          },
          {
            clientName: 'Angelina Jolie',
            date: new Date(),
          },
          {
            clientName: 'Angelina Jolie',
            date: new Date(),
          },
          {
            clientName: 'Angelina Jolie',
            date: new Date(),
          },
          {
            clientName: 'Angelina Jolie',
            date: new Date(),
          },
          {
            clientName: 'Angelina Jolie',
            date: new Date(),
          },
          {
            clientName: 'Angelina Jolie',
            date: new Date(),
          },
          {
            clientName: 'Angelina Jolie',
            date: new Date(),
          },
          {
            clientName: 'Angelina Jolie',
            date: new Date(),
          },
          {
            clientName: 'Angelina Jolie',
            date: new Date(),
          },
          {
            clientName: 'Angelina Jolie',
            date: new Date(),
          },
          {
            clientName: 'Angelina Jolie',
            date: new Date(),
          },
          {
            clientName: 'Angelina Jolie',
            date: new Date(),
          },
          {
            clientName: 'Angelina Jolie',
            date: new Date(),
          },
          {
            clientName: 'Angelina Jolie',
            date: new Date(),
          },
          {
            clientName: 'Angelina Jolie',
            date: new Date(),
          },
          {
            clientName: 'Angelina Jolie',
            date: new Date(),
          },
          {
            clientName: 'Angelina Jolie',
            date: new Date(),
          },
          {
            clientName: 'Angelina Jolie',
            date: new Date(),
          },
          {
            clientName: 'Angelina Jolie',
            date: new Date(),
          },
          {
            clientName: 'Angelina Jolie',
            date: new Date(),
          },
          {
            clientName: 'Angelina Jolie',
            date: new Date(),
          },
          {
            clientName: 'Angelina Jolie',
            date: new Date(),
          },
          {
            clientName: 'Angelina Jolie',
            date: new Date(),
          },
          {
            clientName: 'Angelina Jolie',
            date: new Date(),
          },
          {
            clientName: 'Angelina Jolie',
            date: new Date(),
          },
          {
            clientName: 'Angelina Jolie',
            date: new Date(),
          },
          {
            clientName: 'Angelina Jolie',
            date: new Date(),
          },
          {
            clientName: 'Angelina Jolie',
            date: new Date(),
          },
          {
            clientName: 'Angelina Jolie',
            date: new Date(),
          },
          {
            clientName: 'Angelina Jolie',
            date: new Date(),
          },
          {
            clientName: 'Angelina Jolie',
            date: new Date(),
          },
          {
            clientName: 'Angelina Jolie',
            date: new Date(),
          },
          {
            clientName: 'Angelina Jolie',
            date: new Date(),
          },
          {
            clientName: 'Angelina Jolie',
            date: new Date(),
          },
          {
            clientName: 'Angelina Jolie',
            date: new Date(),
          },
          {
            clientName: 'Angelina Jolie',
            date: new Date(),
          },
          {
            clientName: 'Angelina Jolie',
            date: new Date(),
          },
          {
            clientName: 'Angelina Jolie',
            date: new Date(),
          },
          {
            clientName: 'Angelina Jolie',
            date: new Date(),
          },
          {
            clientName: 'Angelina Jolie',
            date: new Date(),
          },
          {
            clientName: 'Angelina Jolie',
            date: new Date(),
          },
          {
            clientName: 'Angelina Jolie',
            date: new Date(),
          },
          {
            clientName: 'Angelina Jolie',
            date: new Date(),
          },
          {
            clientName: 'Angelina Jolie',
            date: new Date(),
          },
          {
            clientName: 'Angelina Jolie',
            date: new Date(),
          },
          {
            clientName: 'Angelina Jolie',
            date: new Date(),
          },
        ],
        calendar: {},
        selection: null,
        sendUntil: null,
        showDate: false,
        sendEach: null,
        showError: false
      }
    },

    computed: {
      selectionType() {
        switch (this.selection) {
          case 0:
            return 'days';
          case 1:
            return 'weeks';
          case 2:
            return 'months';
          case 3:
          default:
            return 'years';
        }
      }
    },

    methods: {
      openDialog(calendar) {
        this.calendar = calendar
        this.dialog = true
      },

      sendReminder() {
        if(!this.validate()) {
          this.showError = true
          return
        }

        axios.post('backend-route', {calendar: this.calendar, selection: this.selection, sendUntil: this.sendUntil, sendEach: this.sendEach})
        this.showError = false
        this.dialog = false
      },

      parseDate(date) {
        return date.getFullYear() + '-' + ((date.getMonth() + 1) > 9 ? '' : '0') + (date.getMonth() + 1) + (date.getDate() > 9 ? '' : '0') + '-' + date.getDate() + ' ' + date.getHours() + ':' + date.getMinutes();
      },

      validate() {
        return !(this.selection === null || !this.sendUntil);
      }
    }
  }
</script>
