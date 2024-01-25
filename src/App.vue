<script setup>
import { ref, computed, onMounted } from "vue"
import "./css/style.css"
import {
  Chart,
  BarElement,
  BarController,
  CategoryScale,
  LinearScale,
} from "chart.js"
Chart.register(BarElement, BarController, CategoryScale, LinearScale)

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
]

let chartData = groups.darkTetrad

// 回答を格納する配列
const answers = ref(
  new Array(groups.flatMap((group) => group.questions).map(() => null))
)
//回答の配列をコピー
const copiedAnswers = ref([])
// chart.js
const canvasRef = ref(null)
const drawChart = () => {
  if (canvasRef.value === null) return
  const canvas = canvasRef.value.getContext("2d")
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
          suggestedMax: 12,
        },
      },
    },
  })
}
// マウントされたらチャートを描画
onMounted(() => {
  drawChart()
})

// 診断結果を計算する関数
const calculateScores = () => {
  // chartがすでにあった場合は描き換える
  if (myChart) {
    myChart.destroy()
  }

  const scores = []
  for (let i = 0; i < groups.length; i++) {
    let sum = 0
    for (let j = 0; j < groups[i].questions.length; j++) {
      sum += copiedAnswers.value[i * groups[i].questions.length + j]
    }
    scores[i] = sum
    chartData = scores
  }
  drawChart()
  return scores
}

// drawChart();
// calculateScoresが変更されたら更新
const scores = computed(() => calculateScores())
// 送信された時の処理
const submitted = ref(false)
const submit = () => {
  submitted.value = true
  copiedAnswers.value = [...answers.value]
}
</script>
<template>
  <div class="container wrapper">
    <div class="title-wrapper">
      <h1 class="main-title fz28">人格診断テスト</h1>
    </div>
    <form @submit.prevent="submit">
      <div v-for="(group, index) in groups" :key="index" class="group">
        <h2 class="question-title fz24">設問{{ index + 1 }}</h2>
        <div v-for="(question, i) in group.questions" :key="i" class="question">
          <p class="question-text fz20">{{ question.text }}</p>
          <div class="option-wrapper">
            <div
              class="option-loop"
              v-for="(option, j) in question.options"
              :key="j"
            >
              <div class="radio-wrapper">
                <div class="label-wrapper">
                  <label class="label">
                    <input
                      class="radio-button"
                      type="radio"
                      :name="`question${index * group.questions.length + i}`"
                      :value="option.value"
                      v-model="answers[index * group.questions.length + i]"
                      required
                    />
                    <span class="label-button"></span>
                  </label>
                </div>
                <span class="label-text">{{ option.label }}</span>
              </div>
            </div>
          </div>
        </div>
      </div>
      <input
        v-if="!submitted"
        class="submit-button"
        type="submit"
        value="結果を見る"
      />
    </form>
    <div v-if="!submitted" class="before-submit-text">
      <p class="fz24">ここに診断結果が表示されます。</p>
    </div>
    <div class="chart">
      <canvas v-show="submitted" ref="canvasRef"></canvas>
    </div>
    <div class="submitted" v-if="submitted">
      <div v-for="(score, index) in scores" :key="index">
        <p>
          設問{{ index + 1 }}({{ groups[index].darkTetrad }})の結果は{{
            score
          }}点です。
        </p>
      </div>

      <div class="result">
        <div class="narcissism">
          <h3>あなたのナルシシズム傾向</h3>
          <p v-if="scores[0] <= 3">
            あなたはナルシシズムの傾向がほとんどありません。あなたは自分の価値を過大評価せず、他人の評価にも左右されません。あなたは自分の欠点を認めることができ、他人の成功を素直に祝えます。
          </p>
          <p v-else-if="scores[0] >= 4 && scores[0] <= 6">
            あなたはナルシシズムの傾向が少しあります。あなたは自分に自信を持ち、自分の能力や魅力をアピールすることがあります。あなたは他人の評価を気にすることがあり、自分の欠点を隠そうとすることがあります。
          </p>
          <p v-else-if="scores[0] >= 7 && scores[0] <= 9">
            あなたはナルシシズムの傾向がかなりあります。あなたは自分の価値を過大評価し、他人を見下したり、妬んだりすることがあります。あなたは自分の能力や魅力を過剰にアピールすることがあり、他人の評価に敏感です。あなたは自分の欠点を認めることができず、他人のせいにすることがあります。
          </p>
          <p v-else-if="scores[0] >= 10 && scores[0] <= 12">
            あなたはナルシシズムの傾向が非常に強くあります。あなたは自分の価値を極端に過大評価し、他人を軽蔑したり、侮辱したりすることがあります。あなたは自分の能力や魅力を強引にアピールすることがあり、他人の評価に執着します。あなたは自分の欠点を絶対に認めないで、他人を責めることがあります。
          </p>
        </div>
        <div class="machiavellianism">
          <h3>あなたのマキャベリアニズム傾向</h3>
          <p v-if="scores[1] <= 3">
            あなたはマキャベリアニズムの傾向がほとんどありません。あなたは他人に対して誠実で、正直で、信頼できます。あなたは自分の目的のためには手段を選び、他人を利用したり、騙したりすることはしません。
          </p>
          <p v-else-if="scores[1] >= 4 && scores[1] <= 6">
            あなたはマキャベリアニズムの傾向が少しあります。あなたは他人に対して慎重で、計算高いことがあります。あなたは自分の目的のためには手段を選ばないこともあり、他人を利用したり、騙したりすることもあります。
          </p>
          <p v-else-if="scores[1] >= 7 && scores[1] <= 9">
            あなたはマキャベリアニズムの傾向がかなりあります。あなたは他人に対して不誠実で、狡猾で、信用できません。あなたは自分の目的のためには何でもすることがあり、他人を利用したり、騙したりすることが多いです。
          </p>
          <p v-else-if="scores[1] >= 10 && scores[1] <= 12">
            あなたはマキャベリアニズムの傾向が非常に強くあります。あなたは他人に対して裏切りで、陰険で、信用できないです。あなたは自分の目的のためには何でもすることができ、他人を利用したり、騙したりすることが常です。
          </p>
        </div>
        <div class="psychopathy">
          <h3>あなたのサイコパシー傾向</h3>
          <p v-if="scores[2] <= 3">
            あなたはサイコパシーの傾向がほとんどありません。あなたは他人の感情に共感でき、自分の感情にもコントロールできます。あなたは自分の行動に責任を持ち、社会的なルールや道徳に従います。
          </p>
          <p v-else-if="scores[2] >= 4 && scores[2] <= 6">
            あなたはサイコパシーの傾向が少しあります。あなたは他人の感情に共感できることもあれば、無関心であることもあります。あなたは自分の感情にもコントロールできることもあれば、衝動的になることもあります。あなたは自分の行動に責任を持つこともあれば、社会的なルールや道徳を無視することもあります。
          </p>
          <p v-else-if="scores[2] >= 7 && scores[2] <= 9">
            あなたはサイコパシーの傾向がかなりあります。あなたは他人の感情に共感できず、自分の感情にもコントロールできません。あなたは自分の行動に責任を持たず、社会的なルールや道徳を軽視します。
          </p>
          <p v-else-if="scores[2] >= 10 && scores[2] <= 12">
            あなたはサイコパシーの傾向が非常に強くあります。あなたは他人の感情に完全に無関心で、自分の感情にも全くコントロールできないです。あなたは自分の行動に絶対に責任を持たないで、社会的なルールや道徳を完全に無視します。
          </p>
        </div>
        <div class="sadism">
          <h3>あなたのサディズム傾向</h3>
          <p v-if="scores[3] <= 3">
            あなたはサディズムの傾向がほとんどありません。あなたは他人を傷つけたり、苦しめたりすることを嫌います。あなたは他人の苦痛や恐怖を見ると、同情したり、助けたりします。
          </p>
          <p v-else-if="scores[3] >= 4 && scores[3] <= 6">
            あなたはサディズムの傾向が少しあります。あなたは他人を傷つけたり、苦しめたりすることを楽しんだり、興味を持ったりすることがあります。あなたは他人の苦痛や恐怖を見ると、無関心だったり、好奇心を持ったりします。
          </p>
          <p v-else-if="scores[3] >= 7 && scores[3] <= 9">
            あなたはサディズムの傾向がかなりあります。あなたは他人を傷つけたり、苦しめたりすることを楽しみ、探求します。あなたは他人の苦痛や恐怖を見ると、満足したり、興奮したりします。
          </p>
          <p v-else-if="scores[3] >= 10 && scores[3] <= 12">
            あなたはサディズムの傾向が非常に強くあります。あなたは他人を傷つけたり、苦しめたりすることを熱狂的に楽しみ、追求します。あなたは他人の苦痛や恐怖を見ると、歓喜したり、狂喜したりします。
          </p>
        </div>
      </div>
      <div>
        <h2>ダークテトラッドの種類</h2>
        <h3>ナルシシズムの特徴</h3>
        <p>
          ナルシシズムとは、自分が偉大だと認識し、他者を支配する権利があると認識するパーソナリティ特性です。ナルシシストは自己中心的で、自分の欲求や利益を優先し、他人の感情やニーズに無関心です。ナルシシストは自分に対する賞賛や承認を求め、自分の能力や魅力を過大評価し、自分の欠点や失敗を認めません。ナルシシストは自分の自尊心を守るために、他人を批判したり、嫉妬したり、嘘をついたり、操ったりすることがあります。
        </p>
        <h3>ナルシシズムの直し方</h3>
        <p>
          自分の感情や思考に正直に向き合うこと。自分の弱さや過ちを認めることができれば、自分を変えるきっかけになります。
        </p>
        <p>
          他人の視点や感情を尊重すること。他人の意見や感情を聞くことで、自分の考え方や行動が他人にどのような影響を与えているかを理解できます。
        </p>
        <p>
          自分の価値を他人や物事に依存しないこと。自分の価値は他人や物事によって決まるのではなく、自分自身によって決まります。自分の長所や短所を受け入れることで、自分に自信を持つことができます。
        </p>
        <h3>マキャベリアニズムの特徴</h3>
        <p>
          マキャベリアニズムとは、他者に対して冷淡で、操作的で、搾取的な行動をとるパーソナリティ特性です。マキャベリアニストは自分の目的のために手段を選ばず、道徳や倫理にとらわれません。マキャベリアニストは他人を信用せず、自分の利益のために他人を利用したり、騙したり、裏切ったりします。マキャベリアニストは自分の計画や戦略を隠し、自分の立場や影響力を高めるために、他人の弱点や秘密を利用します。
        </p>
        <h3>マキャベリアニズムの直し方</h3>
        <p>
          他人との信頼関係を築くこと。他人との信頼関係は、自分の目的を達成するだけでなく、自分の幸福や満足にも重要です。他人との信頼関係を築くためには、他人に対して誠実で、協力的で、親切であることが必要です。
        </p>
        <p>
          他人の価値や貢献を認めること。他人の価値や貢献を認めることで、他人との関係を改善することができます。他人の価値や貢献を認めることで、自分も他人から認められやすくなります。
        </p>
        <p>
          自分の行動に責任を持つこと。自分の行動に責任を持つことで、自分の行動が他人にどのような影響を与えているかを意識することができます。自分の行動に責任を持つことで、自分の行動を改善することができます。
        </p>

        <h3>サイコパシーの特徴</h3>
        <p>
          サイコパシーとは、鈍感で共感や自責感に欠け、衝動的な行動をとるパーソナリティ特性です。サイコパスは他人を自由に使ったり捨てたりしていい物体と見なし、他人の苦痛や恐怖を楽しんだり、無視したりします。サイコパスは自分の行動による結果をあまり気にせず、罪の意識や恥といった感情もありません。サイコパスは優れた説得者で、他人の皮膚の下に潜り込み、望むものを手に入れるために他人を操ります。サイコパスは反社会的行動や犯罪を起こす可能性が高く、精神疾患として診断されることもあります。
        </p>
        <h3>サイコパシーの直し方</h3>
        <p>
          専門家の助けを求めること。サイコパシーは重度の精神障害であり、自力で治すのはほぼ不可能です。精神科医や心理療法士などの専門家に相談することで、自分の問題に対処する方法を学ぶことができます。
        </p>
        <p>
          他人の感情や思考を理解しようとすること。他人の感情や思考を理解しようとすることで、自分の感情や思考を豊かにすることができます。他人の感情や思考を理解しようとすることで、他人との関係を改善することができます。
        </p>
        <p>
          自分の感情や衝動をコントロールすること。自分の感情や衝動をコントロールすることで、自分の行動に責任を持つことができます。自分の感情や衝動をコントロールすることで、自分の行動を改善することができます。
        </p>

        <h3>サディズムの特徴</h3>
        <p>
          サディズムとは、他者の苦痛を見ると喜びを感じるパーソナリティ特性です。サディストは他人を傷つけたり、苦しめたりすることを楽しみ、自分の支配力や優位性を示すことを好みます。サディストは自分の残酷さに気づいていることもあれば、気づいていないこともあります。サディストは他人の感情やニーズに無関心で、自分の欲求や快楽を優先します。サディズムはダークトライアドの拡大として提案された第4の特性で、ダークトライアドと高い相関があります
        </p>
        <h3>サディズムの直し方</h3>
        <p>
          自分の感情や思考に正直に向き合うこと。自分の感情や思考に正直に向き合うことで、自分がなぜ他人の苦痛に喜びを感じるのかを理解することができます。自分がなぜ他人の苦痛に喜びを感じるのかを理解することで、自分を変えるきっかけになります。
        </p>
        <p>
          他人の感情や思考を尊重すること。他人の感情や思考を尊重することで、他人の苦痛に共感することができます。他人の苦痛に共感することで、他人を苦しめたり、傷つけたりすることをやめることができます。
        </p>
        <p>
          自分の欲望や衝動をコントロールすること。自分の欲望や衝動をコントロールすることで、自分の行動に責任を持つことができます。自分の欲望や衝動をコントロールすることで、自分の行動を改善することができます。
        </p>
        <h3>ダークテトラッドの対処法</h3>
        <p>
          自分がこれらの特性を持っていると気づいた場合は、自分の感情や行動のパターンを客観的に分析し、自分の欠点や問題点を認めることが重要です。自分の感情や行動に責任を持ち、自分の影響力や能力を過大評価しないようにしましょう。自分の自尊心や自己効力感を健全な方法で高めることも大切です。自分の感情や行動について専門家に相談したり、心理療法を受けたりすることも有効です。
        </p>
        <p>
          他人がこれらの特性を持っていると気づいた場合は、その人との関係を見直し、自分の境界や価値観を明確にしましょう。その人に対しては、信頼や親密さを求めず、自分の感情や情報をあまり明かさないようにしましょう。その人の言動に惑わされず、自分の判断や直感を信じましょう。その人からの影響や圧力に抵抗し、自分の権利やニーズを主張しましょう。必要ならば、その人との関係を断ち切ることも考えましょう。自分の感情や体験について、信頼できる人に話したり、専門家に相談したりすることも大切です。
        </p>
        <p>
          これらの特性は、生まれつきのものだけでなく、環境や経験によっても形成されることがあります。そのため、これらの特性を改善することは不可能ではありません。しかし、それには自己認識や自己変革の意志が必要です。自分や他人の幸せのために、これらの特性に気づき、対処することができるようになりましょう。
        </p>
        <p>
          これらの特性は、それぞれ異なるものですが、重なり合う部分もあります。特に共感能力の低さが共通しているといわれています。
        </p>
        <p>
          これらの結果はあくまでも参考程度にとどめていただきますと幸いです。
        </p>
      </div>
    </div>
  </div>

  <footer class="footer">
    <small>&copy; 2023 tkd-120</small>
  </footer>
</template>
