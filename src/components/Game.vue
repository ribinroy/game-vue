<template>
    <div class="game">
        <div class="game_screen_items">
            <div class="data_component credits">
                <span>{{ credits }}</span>
            </div>
            <div class="data_component time">
                <span>{{ time }}</span>
            </div>
            <div class="data_component highscore">
                <span>{{ highscore }}</span>
            </div>
            <div class="data_component life">
                <span>{{ life }}</span>
            </div>
            <div class="score">{{ score }}</div>
        </div>
    </div>
</template>

<script>
export default {
    name: 'Game',
    props: {
        msg: String,
    },
    data: function () {
        return {
            credits: 1,
            time: '00:30:00',
            highscore: 51,
            life: 2,
            score: 100,
        };
    },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
.game {
    width: 100%;
    height: 100%;

    .game_screen_items {
        position: absolute;
        width: 100%;
        height: 100%;
        top: 0;
        left: 0;

        .score {
            width: 100%;
            height: 100%;
            text-align: left;
            font-size: 500px;
            color: #fab612;
            display: flex;
            align-items: center;
            justify-content: center;
            -webkit-text-stroke-width: 8px;
            -webkit-text-stroke-color: #fff;
            text-shadow: 0px 0px 30px #000;
            letter-spacing: 50px;
        }

        .data_component {
            width: 500px;
            height: 180px;
            background-repeat: no-repeat;
            position: absolute;
            background-position: right;

            span {
                letter-spacing: 3px;
                color: #fff;
                position: absolute;
                font-size: 50px;
                right: 20px;
                bottom: 54px;
                width: 50%;
                text-align: center;
            }
        }
        .time {
            background-image: url('./../assets/SVG/time.svg');
            right: 50px;
            top: 20px;
        }
        .life {
            background-image: url('./../assets/SVG/life.svg');
            right: 50px;
            bottom: 20px;
        }
        .highscore {
            background-image: url('./../assets/SVG/highscore.svg');
            left: -10px;
            bottom: 20px;
        }
        .credits {
            background-image: url('./../assets/SVG/credits.svg');
            left: -140px;
            top: 20px;

            span {
                width: 30%;
            }
        }
    }
}
</style>
