<script setup>
import { ref, computed, onMounted } from "vue";
import {
  Chart,
  BarElement,
  BarController,
  CategoryScale,
  LinearScale,
} from "chart.js";
Chart.register(BarElement, BarController, CategoryScale, LinearScale);

const groups = [
  {
    darkTetrad: "ナルシシズム",
    questions: [
      {
        text: "自分は特別で優れていると思う",
        options: [
          {
            label: "同意する",
            value: 4,
          },
          {
            label: "少し同意する",
            value: 3,
          },
          {
            label: "どちらでもない",
            value: 2,
          },
          {
            label: "あまり同意しない",
            value: 1,
          },
          {
            label: "同意しない",
            value: 0,
          },
        ],
      },
      {
        text: "自分のことを認めてほしいと思う",
        options: [
          {
            label: "同意する",
            value: 4,
          },
          {
            label: "少し同意する",
            value: 3,
          },
          {
            label: "どちらでもない",
            value: 2,
          },
          {
            label: "あまり同意しない",
            value: 1,
          },
          {
            label: "同意しない",
            value: 0,
          },
        ],
      },
      {
        text: "他人の感情やニーズに対して関心がない",
        options: [
          {
            label: "同意する",
            value: 4,
          },
          {
            label: "少し同意する",
            value: 3,
          },
          {
            label: "どちらでもない",
            value: 2,
          },
          {
            label: "あまり同意しない",
            value: 1,
          },
          {
            label: "同意しない",
            value: 0,
          },
        ],
      },
    ],
  },
  {
    darkTetrad: "マキャベリアニズム",
    questions: [
      {
        text: "目的を達成するには手段を選ばない",
        options: [
          {
            label: "同意する",
            value: 4,
          },
          {
            label: "少し同意する",
            value: 3,
          },
          {
            label: "どちらでもない",
            value: 2,
          },
          {
            label: "あまり同意しない",
            value: 1,
          },
          {
            label: "同意しない",
            value: 0,
          },
        ],
      },
      {
        text: "他人をだましたり操作するのが得意だと思う",
        options: [
          {
            label: "同意する",
            value: 4,
          },
          {
            label: "少し同意する",
            value: 3,
          },
          {
            label: "どちらでもない",
            value: 2,
          },
          {
            label: "あまり同意しない",
            value: 1,
          },
          {
            label: "同意しない",
            value: 0,
          },
        ],
      },
      {
        text: "道徳や倫理に対し関心を持たない",
        options: [
          {
            label: "同意する",
            value: 4,
          },
          {
            label: "少し同意する",
            value: 3,
          },
          {
            label: "どちらでもない",
            value: 2,
          },
          {
            label: "あまり同意しない",
            value: 1,
          },
          {
            label: "同意しない",
            value: 0,
          },
        ],
      },
    ],
  },
  {
    darkTetrad: "サイコパシー",
    questions: [
      {
        text: "社会的な法や規則に従わないことがある",
        options: [
          {
            label: "同意する",
            value: 4,
          },
          {
            label: "少し同意する",
            value: 3,
          },
          {
            label: "どちらでもない",
            value: 2,
          },
          {
            label: "あまり同意しない",
            value: 1,
          },
          {
            label: "同意しない",
            value: 0,
          },
        ],
      },
      {
        text: "感情が薄く、恐怖や罪悪感を感じない",
        options: [
          {
            label: "同意する",
            value: 4,
          },
          {
            label: "少し同意する",
            value: 3,
          },
          {
            label: "どちらでもない",
            value: 2,
          },
          {
            label: "あまり同意しない",
            value: 1,
          },
          {
            label: "同意しない",
            value: 0,
          },
        ],
      },
      {
        text: "他人に対して冷淡で無関心である",
        options: [
          {
            label: "同意する",
            value: 4,
          },
          {
            label: "少し同意する",
            value: 3,
          },
          {
            label: "どちらでもない",
            value: 2,
          },
          {
            label: "あまり同意しない",
            value: 1,
          },
          {
            label: "同意しない",
            value: 0,
          },
        ],
      },
    ],
  },
  {
    darkTetrad: "サディズム",
    questions: [
      {
        text: "他人に苦痛や損害を与えることに喜びを感じる",
        options: [
          {
            label: "同意する",
            value: 4,
          },
          {
            label: "少し同意する",
            value: 3,
          },
          {
            label: "どちらでもない",
            value: 2,
          },
          {
            label: "あまり同意しない",
            value: 1,
          },
          {
            label: "同意しない",
            value: 0,
          },
        ],
      },
      {
        text: "他人の恐怖や苦しみを見ることに興奮する",
        options: [
          {
            label: "同意する",
            value: 4,
          },
          {
            label: "少し同意する",
            value: 3,
          },
          {
            label: "どちらでもない",
            value: 2,
          },
          {
            label: "あまり同意しない",
            value: 1,
          },
          {
            label: "同意しない",
            value: 0,
          },
        ],
      },
      {
        text: "他人を支配したり支配されたりすることに魅力を感じる",
        options: [
          {
            label: "同意する",
            value: 4,
          },
          {
            label: "少し同意する",
            value: 3,
          },
          {
            label: "どちらでもない",
            value: 2,
          },
          {
            label: "あまり同意しない",
            value: 1,
          },
          {
            label: "同意しない",
            value: 0,
          },
        ],
      },
    ],
  },
];

let chartData = groups.darkTetrad;

// 回答を格納する配列
const answers = ref(
  new Array(groups.flatMap((group) => group.questions).map(() => null))
);
//回答の配列をコピー
const copiedAnswers = ref([]);
// chart.js
const canvasRef = ref(null);
const drawChart = () => {
  if (canvasRef.value === null) return;
  const canvas = canvasRef.value.getContext("2d");
  window.myChart = new Chart(canvas, {
    type: "bar",
    data: {
      labels: [
        "ナルシシズム",
        "マキャベリアニズム",
        "サイコパシー",
        "サディズム",
      ],
      datasets: [
        {
          label: "# of Votes",
          data: chartData,
          backgroundColor: "rgba(164, 64, 201, 0.616)",
        },
      ],
    },
    options: {
      scales: {
        y: {
          suggestedMin: 12,
          // suggestedMax: 20,
        },
      },
    },
  });
};
// マウントされたらチャートを描画
onMounted(() => {
  drawChart();
});

// 診断結果を計算する関数
const calculateScores = () => {
  // chartがすでにあった場合は描き換える
  if (myChart) {
    myChart.destroy();
  }

  const scores = [];
  for (let i = 0; i < groups.length; i++) {
    let sum = 0;
    for (let j = 0; j < groups[i].questions.length; j++) {
      // console.log(groups[i].questions.length);
      sum += copiedAnswers.value[i * groups[i].questions.length + j];
    }
    scores[i] = sum;
    chartData = scores;
  }
  drawChart();
  return scores;
};

// drawChart();
// calculateScoresが変更されたら更新
const scores = computed(() => calculateScores());
// 送信された時の処理
const submitted = ref(false);
const submit = () => {
  submitted.value = true;
  copiedAnswers.value = [...answers.value];
};
</script>
<template>
  <div class="container">
    <h1>人格診断テスト</h1>
    <form @submit.prevent="submit">
      <div v-for="(group, index) in groups" :key="index" class="group">
        <h2>設問{{ index + 1 }}</h2>
        <div v-for="(question, i) in group.questions" :key="i" class="question">
          <p>{{ question.text }}</p>
          <div class="option">
            <label v-for="(option, j) in question.options" :key="j">
              <input
                type="radio"
                :name="`question${index * group.questions.length + i}`"
                :value="option.value"
                v-model="answers[index * group.questions.length + i]"
                required
              />
              {{ option.label }}
            </label>
          </div>
        </div>
      </div>
      <input type="submit" value="結果を見る" />
    </form>
    <div v-if="submitted">
      <h2>診断結果を表示する</h2>
      <div v-for="(score, index) in scores" :key="index">
        <p>
          設問{{ index + 1 }}({{ groups[index].darkTetrad }})の結果は{{
            score
          }}点です。
        </p>
      </div>
      <div>
        <h2>ダークテトラッドの種類</h2>
        <h3>ナルシシズムの特徴</h3>
        <p>
          自分が優れていると過剰に思い込み、他人を見下したり支配したりする傾向があります。自己愛が強く、自尊心や、エゴが肥大化しています。自分を美しく飾るものに執着して、優越感を感じやすいです。他人の評価や承認を求める一方で、共感や感謝の気持ちにかけています。
        </p>
        <h3>マキャベリアニズムの特徴</h3>
        <p>
          自分の目的のためには手段を選ばず、他人を利用したり操ったりする傾向があります。冷淡で、道徳観に関して無関心です。自分の利益を最優先に考え、他人の感情や立場を考慮しません
        </p>
        <h3>サイコパシーの特徴</h3>
        <p>
          他人に対して共感や罪の意識がなく、無責任で衝動的な行動をとる傾向があります。反社会的で、法や規則を守らず、暴力や犯罪に走りやすいです。自分の欲望や快楽を満たすために、他人を傷つけたり危険にさらしたりすることもあります。
        </p>
        <h3>サディズムの特徴</h3>
        <p>
          他人を苦しめたり傷つけることに快楽や喜びを感じる傾向があります。残酷で、他人の痛みや恐怖を楽しんだり、自分の力を見せつけたりします。自分の欲求を満たすために、他人を虐待したり、拷問したりすることもあります。
        </p>
        <p>
          これらの特性は、それぞれ異なるものですが、重なり合う部分もあります。特に共感能力の低さが共通しているといわれています。また、これらの特性は、生まれつきの要因と環境要因の両方によって形成されると考えられています。
        </p>
        <p>上記は、ダークテトラッドの特徴を断定するものではございません。</p>
      </div>
    </div>
    <div v-show="submitted" class="chart">
      <canvas ref="canvasRef"></canvas>
    </div>
  </div>
</template>
