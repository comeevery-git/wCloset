<template>
  <div class="hello_area">
    <div class="hello">
      <h1>{{ msg }}</h1>
      Need a set of equal width and height cards that aren’t attached to one another? Use card decks.
      <font-awesome-icon icon="user-secret" />
      <div class="craw_area">
        <p class="_crew_title">
          위치
        </p>
        <div>
          <font-awesome-icon icon="user-secret" />
        </div>
        <p class="_crew_title">
          현재온도
        </p>
        <div>
          <font-awesome-icon icon="user-secret" />
        </div>
      </div>


      <!-- 선호 스타일 조사 영역 -->
      <div @click="styleCdChange()">
        <button>OPEN!</button>
      </div>
      <div class="card_area">
        <div class="card-group">
          <div class="card">
            <div class="card-body">
              <h5 class="card-title">Card title</h5>
              <p class="card-text">온도에 알맞아요.</p>
              <p class="card-text">온도에 맞지 않아요.</p>
              <img class="card-img-top" src="temp.png" alt="Card image cap">
            </div>
            <div class="card-footer">
              <small class="text-muted">캐쥬얼, 21도, 노란계열</small>
            </div>
          </div>
          <div class="card">
            <div class="card-body">
              <h5 class="card-title">Card title</h5>
              <img class="card-img-top" src="temp.png" alt="Card image cap">
            </div>
            <div class="card-footer">
              <small class="text-muted">로맨틱, 18도, 붉은계열</small>
            </div>
          </div>
          <div class="card">
            <div class="card-body">
              <h5 class="card-title">Card title</h5>            
              <img class="card-img-top" src="temp.png" alt="Card image cap">
            </div>
            <div class="card-footer">
              <small class="text-muted">출근, 5도, 갈색계열</small>
            </div>
          </div>
        </div>
      </div>
    </div>

    
    <!-- 선호 스타일 조사 영역 -->
    <div :class="{ notion_area:isStyleCdChange }" v-show="isStyleCdChange">
      <span>좋아하는 연예인을 입력해주세요!</span>
      <br>
      <span>{{ notion }}</span>
      <br>
      <input type="text" v-model="styleCd">
    </div>


    <!-- 공지사항 영역 -->
    <div class="notice_area">
      <b-table-simple hover small caption-top responsive>
        <caption class="_caption">&nbsp;공지사항</caption>
        <b-thead>
          <b-tr>
            <b-th scope="col">번호</b-th>
            <b-th scope="col">제목</b-th>
            <b-th scope="col">작성일</b-th>
            <b-th scope="col">작성자</b-th>
          </b-tr>
        </b-thead>
        <b-tbody id="items" v-for="item in items" :key="item.id">
          <b-tr>
            <b-td>{{ item.id }}</b-td>
            <b-td>{{ item.title }}</b-td>
            <b-td>2021-10-17 12:49:00</b-td>
            <b-td>강수희</b-td>
          </b-tr>
        </b-tbody>
      </b-table-simple>
    </div>


  </div>
</template>

<script>
import _ from "lodash"

export default {
  name: 'HelloWorld',
  props: {
    msg: String
  },
  data() {
    return {
      debounceGetAnswer: null,
      notion: '',
      styleCd: '',
      colorCd: '',
      // fields: ['번호', '제목', '작성일','작성자'],
      items: [
        {
          id: 1,
          title: "테이블 컴포넌트의 사용",
          content: ""
        },
        {
          id: 2,
          title: "[시스템 점검안내] 2021-10-18 00:00 ~ 01:00",
          content: ""
        },
        {
          id: 3,
          title: "[시스템 점검안내] 2021-10-17 00:00 ~ 01:00",
          content: ""
        },
      ],
      isStyleCdChange: false
    }
  },
  watch: {
    styleCd () {
      this.notion = "당신의 스타일 코드는..."
      this.debounceGetAnswer();
    }
  },
  created() {
    this.debounceGetAnswer = _.debounce(this.getAnswer, 500)
  },
  methods: {
    getAnswer() {
      const self = this
        if(self.styleCd.length >= 2) {
          self.notion = '아하!'+self.styleCd+'을 좋아하시는 군요.';
        }
    },
    noticeDetail(no) {
      alert(no);
      this.noticeDetailModal(no);
    },
    noticeDetailModal(no) {
      // TODO : 공지사항 상세 페이지
      alert("상세 모달 띄우기!" + no);
    },
    styleCdChange() {
      self.isStyleCdChange = !self.isStyleCdChange;
      console.log("=============="+self.isStyleCdChange);
    }
  },
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}

.hello_area {
  /* font-family: 'Gaegu', cursive; */
}

.card_area {
  font-family: 'Gaegu', cursive;
  padding: 1em;
  margin-top: 2em;
  margin-bottom: 2em;
}

.craw_area {
  width: 30em;
  margin-left: auto;
  margin-right: auto;
  font-family: 'Gaegu', cursive;
  display: grid;
}
._crew_title {
  margin-left: 8rem;
  margin-top: 1em;
  margin-bottom: -5px;
  color: #41b883;
  text-align: left;
}

.notion_area {
  font-family: 'Gaegu', cursive;
  margin-left: auto;
  margin-right: auto;
  border: 2px solid #41b883;
  box-shadow: 0 1px 0 1px #bec9c4;
  width: fit-content;
  padding: 2rem;
  border-radius: 2rem;
}

.notice_area {
  margin-top: 2rem;
  margin-bottom: 2rem;
  font-size: 12px;
}

._caption {
  color: #41b883;
}


._styleCd_change {
  background-color: red;
}

.green {
  background-color: green;
}

.blue {
  background-color: blue;
}

</style>
