# No Cap News
> 자극적이거나 불쾌함을 일으켜 클릭만을 유도하는 제목을 필터링하여 보여주는 뉴스 어플
>
> [팀 프로젝트(2인): 2022.07.06 ~ 2022.0.0]
> - 디자이너 1명, 프론트엔드 1명
> - 역할) 서비스 기획, 뉴스 API 끌어오기 포함 프론트 구현
>
<!-- > 주소:  -->

***
## Service Info
: 최근 상업적인 목적을 위해 자극적인 제목/내용을 강조하거나 제대로된 정보를 제공하지 않는 뉴스가 많아져, <br>
이에 신뢰를 잃고 피로가 쌓인 사람들을 위한 '군더더기 없이 깔끔하게 뉴스만 제공하는 서비스'

<br>
<!-- 
#### _해당 프로젝트의 서비스는..._
*  -->

***
## Code Info
_Main_
* [News API](https://newsapi.org/v2)에서 카테고리별 뉴스 API 요청(axios)
* `useEffect`를 통해 카테고리 탭메뉴가 변경될 때마다 API 정보 업데이트하기
```javascript
useEffect(() => {
    const fetchData = async () => {
      setLoading(true); // 기사를 받아오는 중

      try {
        const res = await axios.get(`https://newsapi.org/v2/top-headlines?country=kr&category=${category}&apiKey=b1e207f1b83d47a081c09e0040dd68e7`);
        const JsonData = res.data.articles;
        setNews(JsonData);
      }
      catch (err){
        alert(err);
      }

      setLoading(false); // 받아오기 완료/실패
    }
    fetchData();
  },[category]);
```
* 뉴스 정보를 불러오는 동안 로딩중 텍스트 표시
* `map()`을 활용해 뉴스 정보 + 카테고리 표시
* 탭 메뉴: 탭 메뉴를 클릭하면 해당 제목으로 `state(=category)`를 변경해 내용 표시 + 클릭 배경 효과 적용
* 뉴스 이미지가 보이지 않는 경우 default image 표시
```javascript
<Img src={
  news.urlToImage == null
  ? process.env.PUBLIC_URL + '/image/default_img.png'
  : news.urlToImage
}/>
```
***

_Detail_
* 뉴스를 클릭했을 때 해당 뉴스를 자세히 보여주기 위해 Open API 데이터에 id 값 추가 -> id 값을 url의 맨 뒤에 넣어 `useParams()`를 사용할 수 있도록 만듦
```javascript
// detail page를 위한 id값 부여하는 함수
const newsIdSet = () => {
  news.map((a,i) => news[i].source.id = i);
};

// 뉴스를 클릭하면 id 값이 url 경로 맨 뒤에 추가되도록
<NewsItem onClick={() => { navigate('/detail/'+news.source.id) }}>
```

<!-- ***
## 코드 수정 📝
* 


***
## 개선할 사항 🚀
* 

***
#### _* 자세한 실행과정 정리(노션: )_ -->
