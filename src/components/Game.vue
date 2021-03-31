<template>
    <div class="game">
        <button @click="switchScreen()" class="test_button">TEST</button>
        <div
            class="game_screen_items"
            v-if="currentScreen === 'game' || currentScreen === '2 player'"
        >
            <div class="data_component credits">
                <span><v-number v-model="credits"></v-number></span>
            </div>
            <div class="data_component time">
                <span
                    ><div>{{ formatToTime(time) }}</div></span
                >
            </div>
            <div class="data_component highscore">
                <span><v-number v-model="highscore"></v-number></span>
            </div>
            <div class="data_component life">
                <span><v-number v-model="life"></v-number></span>
            </div>
            <div class="score flex_wrap" v-if="currentScreen === 'game'">
                <animated-number
                    :value="score"
                    :formatValue="formatToValue"
                    :duration="300"
                ></animated-number>
            </div>
            <div
                class="score two_player_score flex_wrap"
                v-if="currentScreen === '2 player'"
            >
                <animated-number
                    :value="score"
                    :formatValue="formatToValue"
                    :duration="300"
                ></animated-number>
                \
                <animated-number
                    :value="score"
                    :formatValue="formatToValue"
                    :duration="300"
                ></animated-number>
            </div>
        </div>
        <div
            class="game_screen_items"
            v-if="currentScreen === 'new high score'"
        >
            <div class="flex_wrap">
                <div class="new_highscore_button">NEUER HIGHSCORE!!</div>
            </div>
        </div>
        <div
            class="game_screen_items"
            v-else-if="currentScreen === 'insert coin'"
        >
            <div class="data_component highscore top_only">
                <span><v-number v-model="highscore"></v-number></span>
            </div>
            <div class="flex_wrap">
                <div class="insert_coin_text">
                    Bitte GELD EINWERFEN <br />
                    ODER GAME CARD SCANNEN
                </div>
            </div>
        </div>
    </div>
</template>

<script>
import AnimatedNumber from 'animated-number-vue';
import { VNumber } from '@maxflex/v-number';
export default {
    name: 'Game',
    components: {
        AnimatedNumber,
        VNumber,
    },
    mounted: function () {
        //DEMO CODES
        const _this = this;
        setInterval(() => {
            _this.score += 10;
            _this.life += 1;
            _this.highscore += 8;
        }, 1000);

        const timerInterval = setInterval(() => {
            if (_this.time <= 0) {
                _this.time = 0;
                clearInterval(timerInterval);
            } else _this.time -= 10;
        }, 1);
    },
    data: function () {
        return {
            currentScreen: 'game',
            credits: 999,
            time: 72000, //in milliseconds
            highscore: 51,
            life: 2,
            score: 100,
        };
    },
    methods: {
        formatToValue(value) {
            return `${value.toFixed(0)}`;
        },
        formatToTime(duration) {
            var milliseconds = parseInt((duration % 1000) / 10),
                seconds = parseInt((duration / 1000) % 60),
                minutes = parseInt((duration / (1000 * 60)) % 60),
                hours = parseInt((duration / (1000 * 60 * 60)) % 24);

            hours = hours < 10 ? '0' + hours : hours;
            minutes = minutes < 10 ? '0' + minutes : minutes;
            seconds = seconds < 10 ? '0' + seconds : seconds;

            return (
                +minutes +
                ':' +
                seconds +
                ':' +
                (milliseconds.length == 1 ? '0' + milliseconds : milliseconds)
            );
            // Hours, minutes and seconds
        },
        switchScreen: function () {
            switch (this.currentScreen) {
                case 'game':
                    this.currentScreen = '2 player';
                    break;
                case 'insert coin':
                    this.currentScreen = 'game';
                    break;
                case 'new high score':
                    this.currentScreen = 'insert coin';
                    break;
                case '2 player':
                    this.currentScreen = 'new high score';
                    break;
                default:
                    this.currentScreen = 'insert coin';
                    break;
            }
        },
    },
};
</script>

<style scoped lang="scss">
@keyframes comeIn {
    from {
        opacity: 0;
        transform: scale(0);
    }
    to {
        opacity: 1;
        transform: scale(1);
    }
}

@keyframes pulsating {
    from {
        transform: scale(1);
    }
    to {
        transform: scale(0.7);
    }
}

@keyframes pulsatingSmall {
    from {
        transform: scale(1);
    }
    to {
        transform: scale(0.9);
    }
}

@keyframes heartBeat {
    0% {
        transform: scale(1);
    }
    10% {
        transform: scale(0.9);
    }
    20% {
        transform: scale(1);
    }
    100% {
        transform: scale(1);
    }
}

.game {
    width: 100%;
    height: 100%;

    .test_button {
        z-index: 99;
        position: relative;
    }
    .game_screen_items {
        position: absolute;
        width: 100%;
        height: 100%;
        top: 0;
        left: 0;

        .flex_wrap {
            display: flex;
            align-items: center;
            justify-content: center;
            width: 100%;
            height: 100%;
        }

        .new_highscore_button {
            background-image: url('./../assets/SVG/highscore cheer.svg');
            font-size: 110px;
            padding: 210px;
            background-repeat: no-repeat;
            color: #fff;
            background-position: center;
            animation: comeIn 0.5s 1, heartBeat 1s 0.5s infinite alternate;
        }

        .insert_coin_text {
            text-align: center;
            font-size: 180px;
            color: #fab612;
            -webkit-text-stroke-width: 4px;
            -webkit-text-stroke-color: #fff;
            text-shadow: 0px 0px 30px #000;
            line-height: 15rem;
            animation: comeIn 0.5s linear,
                pulsating 1.5s 0.5s infinite alternate;
            // letter-spacing: 50px;
        }

        .score {
            text-align: left;
            font-size: 500px;
            color: #fab612;
            -webkit-text-stroke-width: 8px;
            -webkit-text-stroke-color: #fff;
            text-shadow: 0px 0px 30px #000;
            letter-spacing: 50px;
            animation: comeIn 0.4s 1 ease-in-out,
                pulsatingSmall 2s 0.5s infinite alternate ease-in-out;
        }

        .two_player_score {
            font-size: 350px !important;
        }

        .data_component {
            width: 500px;
            height: 180px;
            background-repeat: no-repeat;
            position: absolute;
            background-position: right;
            animation: comeIn 0.4s 1 ease-in-out;

            span {
                letter-spacing: 3px;
                color: #fff;
                position: absolute;
                font-size: 50px;
                right: 32px;
                bottom: 51px;
                width: 50%;
                text-align: center;
                font-variant-numeric: tabular-nums;
                div {
                    padding: 0 15px;
                }
            }
        }
        .time {
            background-image: url('./../assets/SVG/time.svg');
            right: 50px;
            top: 20px;

            span {
                bottom: 63px;
                right: 15px;
            }
        }
        .life {
            background-image: url('./../assets/SVG/life.svg');
            right: 50px;
            bottom: 20px;

            span {
                width: 30%;
            }
        }
        .highscore {
            background-image: url('./../assets/SVG/highscore.svg');
            left: 40px;
            top: 20px;
            width: 440px;

            &.top_only {
                bottom: auto !important;
                top: 40px;
            }
        }
        .credits {
            background-image: url('./../assets/SVG/credits.svg');
            left: -110px;
            bottom: 20px;

            span {
                width: 30%;
                bottom: 51px;
            }
        }
    }
}
</style>
