<template>
  <div class="hello_area">
    <!-- 버튼 모음 -->
    <div class="button_area">
      <ul>
        <li><button @click="styleCdChange()">스타일 체크</button></li>
        <li><button @click="noticeOpenChange()">공지사항</button></li>
      </ul>  
    </div>
    
    <div class="hello">
      <h1>{{ msg }}</h1>

      <div class="craw_area">
        <div>
          <p class="_craw_title">
            위치
          </p>
          <div>
            서울특별시 중림로 중구
          </div>
          <p class="_craw_title">
            현재온도
          </p>
          <div>
            <font-awesome-icon icon="user-secret" />
            맑음 17°
            <br>
            어제보다 0° 높아요
          </div>
        </div>
        <div class="_craw_week">
          <p class="_craw_title">
            주간온도
          </p>
8° 
09시구름많음
9° 
10시구름많음
11° 
11시흐림
12° 
12시흐림
13° 
13시흐림
        </div>
      </div>

      <!-- 메인 컨텐츠 모음 -->
      <div class="card_area">
        <div class="card-group">
          <div class="card">
            <div class="card-body">
              <h5 class="card-title">Card title</h5>
              <p class="card-text">날씨에 알맞아요.</p>
              <p class="card-text">날씨보다 추워요.</p>
              <p class="card-text">날씨보다 더워요.</p>
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
    <div :class="{ notion_area:isStyleCdChange }" v-if="isStyleCdChange">
      <span>좋아하는 연예인을 입력해주세요!</span>
      <br>
      <span>{{ notion }}</span>
      <br>
      <input type="text" v-model="styleCd">
    </div>


    <!-- 공지사항 영역 -->
    <div :class="{ notice_area:isNoticeOpenChange }" v-if="isNoticeOpenChange">
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
      isStyleCdChange: false,
      isNoticeOpenChange: false
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
        if(this.styleCd.length >= 2) {
          this.notion = '아하!'+this.styleCd+'을 좋아하시는 군요.';
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
      this.isStyleCdChange = !this.isStyleCdChange;
    },
    noticeOpenChange() {
      this.isNoticeOpenChange = !this.isNoticeOpenChange;
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
  margin: 0 0.2em;
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
  width: fit-content;
  text-align-last: center;
  font-family: 'Gaegu', cursive;
  display: table;

  margin-left: auto;
  margin-right: auto;
}
._craw_title {
  margin-bottom: -3px;
  color: #41b883;
  font-weight: bold;
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

.button_area {

}

.button_area button {
  margin-right: 1em;
  border-radius: 2em;
  padding: 0.3em 0.8em 0.3em 0.8em;
  border-color: aliceblue;
  color: #35495e;
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
