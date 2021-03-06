# Korean Zipcode Finder

* 인터넷 우체국 제공 우편번호 찾기 API 를 사용한 우편번호 찾기 gem
* https://biz.epost.go.kr/ui/index.jsp

## 사용법 (Usage)

* Gemfile 에 추가한 후 `bundle install` 한다.

  ```ruby
  gem 'korean_zipcode_finder'
  ```

* 인터넷우체국에서 api_key 를 신청하여 발급받음 (https://biz.epost.go.kr/ui/index.jsp)

* config/initializers/korean_zipcode_finder.rb 파일을 생성한 후 아래와 같이 `api_key` 값을 지정

  ```ruby
  KoreanZipcodeFinder.configure do |config|
    config.api_key = "#{YOUR_API_KEY}"
  end
  ```

* 제대로 동작하는지 확인하기 위해 레일스 콘솔을 열고 아래와 같이 명령을 호출해 본다.

  ```bash
  irb(main):001:0> KoreanZipcodeFinder.find_zipcode('공덕동')
  => [[#<struct Struct::KoreanZipcodeFinder zipcode="04213", zipcode_01="042",
  zipcode_02="213", address="서울특별시 마포구 마포대로 108 (공덕동)",
  original_address="서울특별시 마포구 마포대로 108 (공덕동)">,
  #<struct Struct::KoreanZipcodeFinder zipcode="04213", zipcode_01="042",
  zipcode_02="213", address="서울특별시 마포구 마포대로 108-1 (공덕동)",
  original_address="서울특별시 마포구 마포대로 108-1 (공덕동)">,
  #<struct Struct::KoreanZipcodeFinder zipcode="04213", zipcode_01="042",
  zipcode_02="213", address="서울특별시 마포구 마포대로 108-3 (공덕동)",
  original_address="서울특별시 마포구 마포대로 108-3 (공덕동)">,
  #<struct Struct::KoreanZipcodeFinder zipcode="04146", zipcode_01="041",
  zipcode_02="146", address="서울특별시 마포구 마포대로 109 (공덕동, 롯데캐슬프레지던트)",
  original_address="서울특별시 마포구 마포대로 109 (공덕동, 롯데캐슬프레지던트)">,
  #<struct Struct::KoreanZipcodeFinder zipcode="04213", zipcode_01="042",
  zipcode_02="213", address="서울특별시 마포구 마포대로 110 (공덕동)",
  original_address="서울특별시 마포구 마포대로 110 (공덕동)">,
  #<struct Struct::KoreanZipcodeFinder zipcode="04213", zipcode_01="042",
  zipcode_02="213", address="서울특별시 마포구 마포대로 110-1 (공덕동)",
  original_address="서울특별시 마포구 마포대로 110-1 (공덕동)">,
  #<struct Struct::KoreanZipcodeFinder zipcode="04213", zipcode_01="042",
  zipcode_02="213", address="서울특별시 마포구 마포대로 112 (공덕동)",
  original_address="서울특별시 마포구 마포대로 112 (공덕동)">,
  #<struct Struct::KoreanZipcodeFinder zipcode="04213", zipcode_01="042",
  zipcode_02="213", address="서울특별시 마포구 마포대로 112-4 (공덕동)",
  original_address="서울특별시 마포구 마포대로 112-4 (공덕동)">,
  #<struct Struct::KoreanZipcodeFinder zipcode="04213", zipcode_01="042",
  zipcode_02="213", address="서울특별시 마포구 마포대로 112-5 (공덕동)",
  original_address="서울특별시 마포구 마포대로 112-5 (공덕동)">,
  #<struct Struct::KoreanZipcodeFinder zipcode="04213", zipcode_01="042",
  zipcode_02="213", address="서울특별시 마포구 마포대로 114 (공덕동)",
  original_address="서울특별시 마포구 마포대로 114 (공덕동)">],
  {:totalCount=>"1775", :totalPage=>"178", :countPerPage=>"10", :currentPage=>"1"}]
  ```

## Rails 5 Engine

**기본 설정**

* **application.js** 에서 아래와 같이 추가

  ```javascript
  //= require korean_zipcode_finder/core
  ```

* **application.css** 에서 아래와 같이 추가하거나

  ```css
  *= require korean_zipcode_finder/core
  ```

* 또는 **application.scss** 에서 아래와 같이 추가
  ```scss
  @import "korean_zipcode_finder/core";
  ```

**Twitter Bootstrap v4.1.0 호환**

* **core.css** 파일은 **will_paginate** 젬을 이용한 페이징 링크에 적용할 스타일 클래스가 포함됨.

**html 마크업**

* ".address_area" 클래스를 가진 wrapper 속에 ".zipcode", ".address_01" 클래스를 가진 text_area 생성
* ".find_zipcode_btn" 클래스를 가진 "우편번호 찾기" 링크를 추가

  ![](app/assets/images/address_area.png)

  ```html
  <div class="address_area">
    <div class='form-group'>
      <%= p.label :zip_code %><br />
      <%= p.text_field :zip_code, placeholder: '99999', class: 'zipcode form-control col-4 col-sm-3 col-md-3 d-inline'%>
      <%= link_to '우편번호 찾기', '#', :class => "find_zipcode_btn btn btn-primary ml-2" %>
    </div>
    <div class="form-group">
      <%= p.label :address_1 %><br />
      <%= p.text_field :address_1, placeholder: '메인주소', class: "address_01 form-control mb-2" %>
      <%= p.text_field :address_2, placeholder: '상세주소', class: "address_02 form-control" %>
    </div>
  </div>
  ```

  ![](app/assets/images/search_zipcodes.png)

**적용하기**

자바스크립트 파일에서 아래와 같이 호출하면 됨.

```javascript
new KoreanZipcodeFinder();
```
