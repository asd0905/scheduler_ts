<template>
    <div id="app">
        <JqxScheduler ref="myScheduler"
                      :width="getWidth" :height="600" :source="dataAdapter" :date="date" :view="'weekView'"
                      :resources="resources"
                      :appointmentDataFields="appointmentDataFields" :views="views" :showLegend="true"
                      :dayNameFormat="'abbr'"
        />
    </div>
</template>

<script lang="ts">
    import {Component, Vue} from 'vue-property-decorator';
    import JqxScheduler from 'jqwidgets-scripts/jqwidgets-vue/vue_jqxscheduler.vue';

    declare const jqx: any;
    declare const ensureAppointmentVisible: any;

    @Component({
        components: {
            JqxScheduler,
        },
    })

    export default class App extends Vue {
        private getWidth = '90%';
        private date = new jqx.date(2016, 11, 23);

        private appointmentDataFields =
                {
                    from: 'start',
                    to: 'end',
                    id: 'id',
                    description: 'description',
                    location: 'place',
                    subject: 'subject',
                    resourceId: 'calendar',
                };
        private source: any;
        private resources =
                {
                    colorScheme: 'scheme05',
                    dataField: 'calendar',
                    orientation: 'horizontal',
                    source: new jqx.dataAdapter(this.source),
                };
        private views =
                [
                    {type: 'dayView', showWeekends: false},
                    {type: 'weekView', showWeekends: false},
                    {type: 'monthView'},
                ];
        private dataAdapter: any;

        private beforeCreate() {
            const generateAppointments = () => {
                const appointments = new Array();
                const appointment1 = {
                    id: 'id1',
                    description: 'George brings projector for presentations.',
                    location: '',
                    subject: 'Quarterly Project Review Meeting',
                    calendar: 'Room 1',
                    start: new Date(2016, 10, 23, 9, 0, 0),
                    end: new Date(2016, 10, 23, 16, 0, 0),
                };
                const appointment2 = {
                    id: 'id2',
                    description: '',
                    location: '',
                    subject: 'IT Group Mtg.',
                    calendar: 'Room 2',
                    start: new Date(2016, 10, 24, 10, 0, 0),
                    end: new Date(2016, 10, 24, 15, 0, 0),
                };
                const appointment3 = {
                    id: 'id3',
                    description: '',
                    location: '',
                    subject: 'Course Social Media',
                    calendar: 'Room 1',
                    start: new Date(2016, 10, 27, 11, 0, 0),
                    end: new Date(2016, 10, 27, 13, 0, 0),
                };
                const appointment4 = {
                    id: 'id4',
                    description: '',
                    location: '',
                    subject: 'New Projects Planning',
                    calendar: 'Room 2',
                    start: new Date(2016, 10, 23, 0, 0, 0),
                    end: new Date(2016, 10, 25, 23, 59, 59),
                };
                const appointment5 = {
                    id: 'id5',
                    description: '',
                    location: '',
                    subject: 'Interview with James',
                    calendar: 'Room 1',
                    start: new Date(2016, 10, 25, 15, 0, 0),
                    end: new Date(2016, 10, 25, 17, 0, 0),
                };
                const appointment6 = {
                    id: 'id6',
                    description: '',
                    location: '',
                    subject: 'Interview with Nancy',
                    calendar: 'Room 2',
                    start: new Date(2016, 10, 26, 14, 0, 0),
                    end: new Date(2016, 10, 26, 16, 0, 0),
                };

                appointments.push(appointment1);
                appointments.push(appointment2);
                appointments.push(appointment3);
                appointments.push(appointment4);
                appointments.push(appointment5);
                appointments.push(appointment6);

                return appointments;
            };

            this.source = {
                        dataType: 'array',
                        dataFields: [
                            {name: 'id', type: 'string'},
                            {name: 'description', type: 'string'},
                            {name: 'location', type: 'string'},
                            {name: 'subject', type: 'string'},
                            {name: 'calendar', type: 'string'},
                            {name: 'start', type: 'date'},
                            {name: 'end', type: 'date'},
                        ],
                        id: 'id',
                        localData: generateAppointments(),
                    };

            this.dataAdapter = new jqx.dataAdapter(this.source);
        }

        private mounted() {
            (this.$refs.myScheduler as any).ensureAppointmentVisible('id1');
        }
    }
</script>

<style scoped lang="scss">
    @import '../node_modules/jqwidgets-scripts/jqwidgets/styles/jqx.base.css';

    #app {
        font-family: Avenir, Helvetica, Arial, sans-serif;
        -webkit-font-smoothing: antialiased;
        -moz-osx-font-smoothing: grayscale;
        text-align: center;
        color: #2c3e50;
        margin-top: 60px;
    }


</style>
