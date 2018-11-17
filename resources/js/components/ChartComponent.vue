<script>
    import {Line} from 'vue-chartjs';
    export default {
        extends: Line,
        data(){
            return {
                url: 'http://localhost:8000/products',
                years: [],
                labels: [],
                prices: [],
                data: ''
            }
        },

        methods: {

            getProducts(){
                axios.get(this.url).then((response)=>{
                this.data = response.data;

                    if(this.data){
                        this.data.forEach(element => {
                        this.years.push(element.year);
                        this.labels.push(element.name);
                        this.prices.push(element.price);
                        });
                        this.renderChart({

                            labels: this.years,
                            datasets: [
                                {
                                    label: 'Sales',
                                    backgroundColor: '#ff0000',
                                    data: this.prices
                                }
                            ]
                        }, {responsive: true, maintainAspectRatio: false});

                    } else {

                        console.log('NO DATA');
                    }
                });
            }
        },
        mounted() { //元素已掛載
            this.getProducts();
        }
    }
</script>
