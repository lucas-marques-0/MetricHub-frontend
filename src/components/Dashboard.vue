<template>
    <div id="dashboard">
        <hr>
        <h2>Visualize suas métricas abaixo!</h2>

        <h3>Aqui vai o seu <span class="metric-name">Monthly Recurring Revenue (MRR)</span></h3>
        <canvas id="myChart"></canvas>

        <h3>Aqui vai o seu <span class="metric-name">Churn Rate (CR)</span></h3>
        <canvas id="myChart2"></canvas>
    </div>
</template>

<script>
import Chart from 'chart.js/auto';

export default {
    props: {
        chartDataMRR: { type: Object, required: true },
        chartDataCR: { type: Object, required: true }
    },
    mounted() {
        const createChart = (ctx, data, label) => {
            new Chart(ctx, {
                type: 'bar',
                data: {
                    labels: data.keys,
                    datasets: [{
                        label: label,
                        data: data.values,
                        backgroundColor: 'rgba(65, 22, 127, 0.7)',
                        borderWidth: 1
                    }]
                },
                options: { scales: { y: { beginAtZero: true } } }
            });
        };

        createChart(document.getElementById('myChart'), this.chartDataMRR, 'Monthly Recurring Revenue (MRR)');
        createChart(document.getElementById('myChart2'), this.chartDataCR, 'Churn Rate (CR)');
    }
};
</script>

<style>
#dashboard {
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
}

hr {
    width: 100%;
    border: 1px solid #42167f34; 
}

#dashboard h2 {
    margin-top: 30px;
    background-color: #0D9D68;
    padding: 7px;
    border-radius: 7px;
    color: #fff;
    margin-bottom: 100px;
}


.metric-name {
    background-color: #42167f34;
    padding: 7px;
    border-radius: 7px;
    text-decoration: underline;
}

canvas {
    margin-bottom: 80px;
    margin-top: 30px;
    width: 900px;
    height: 450px;
}

@media screen and (max-width: 900px) {
    canvas {
        width: 95vw !important;
    }

    #dashboard h2 {
        max-width: 90vw;
        text-align: center;
    }

    #dashboard h3 {
        max-width: 90vw;
        text-align: center;
    }
}

@media screen and (max-width: 550px) {
    #dashboard h3 {
        font-size: 0.9em;
    }

    .metric-name {
        background-color: rgba(0, 0, 0, 0);
    }
}

@media screen and (max-width: 350px) {
    #dashboard h2 {
        margin-top: 0px;
        margin-bottom: 60px;
        font-size: 0.9em;
    }

    #dashboard h3 {
        font-size: 0.9em;
    }

    hr {
        margin: 30px 0;
    }
}

</style>
