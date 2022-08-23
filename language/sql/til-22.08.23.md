---
description: PostgreSQL을 기준으로 데이터베이스 구축 과정을 통해 알게 된 것들
---

# TIL(22.08.23)

## Data Type

### Email

* 사용자 이름은 64자 이하로 제한
* 총 문자수 254자 -> VARCHAR(254)

참고

{% embed url="https://www.lifewire.com/is-email-address-length-limited-1171110" %}
이메일
{% endembed %}



### 자동 생성 기본 키

* 보통 `id`를 인덱스로 사용
* `BIGINT GENERATED ALWAYS AS IDENTITY PRIMARY KEY`

참고

{% embed url="https://www.cybertec-postgresql.com/en/uuid-serial-or-identity-columns-for-postgresql-auto-generated-primary-keys/" %}



### 생성, 수정 날짜

* 생성 날짜
  * `TIMESTAMP NOT NULL DEFAULT NOW()` : 현재 시간으로 설정
* 수정 날
  * TIMESTAMP

#### UPDATE TIME TRIGGER

{% tabs %}
{% tab title="1. Function 작성" %}
* 수정일을 자동으로 설정하는 기능
* Table이 여러개여도 column명이 동일하면, 처리 담당할 function은 하나만 만들면 된다.

```sql
create or replace function update_time()
returns trigger as $$
begin
	new.update_time = now();
	return new;
end;
$$ language plpgsql;
```

###
{% endtab %}

{% tab title="2. Trigger 작성" %}
* Trigger는 각 테이블에 Function을 연결시키는 역할
* 무조건 테이블 수 만큼 만들어야 한다.

```sql
create trigger update_trigger
before update on [post]
for each row
execute procedure update_time();
```
{% endtab %}

{% tab title="TEST" %}
<pre class="language-sql"><code class="lang-sql"><strong>INSERT INTO post(title) VALUES ('test');</strong></code></pre>



```sql
update post title = 'test2' where post_id = 1;
```
{% endtab %}
{% endtabs %}



### 전화 번

* `VARCHAR(25)`

참고

{% embed url="https://en.wikipedia.org/wiki/E.164" %}









PostgreSQL에는 VARCHAR2가 없다. VARCHAR가 같은 기능

{% embed url="https://www.postgresqltutorial.com/postgresql-tutorial/postgresql-char-varchar-text/" %}

###

## 웹 어플리케이션의 채팅 알림

~~필자의 개인적 의견입니다~~

메세지를 보내면 알림이 나가야하는데 내가 만드는 것은 앱이 아니기 때문에 notification 기능을 쓰지 못한다.

이때 이메일로 메시지 도착 알림을 보내면 스마트폰에 이메일로 알림이 오니까 notification 기능을 대체할 수 있다고 생각한다. 즉 화면에도 메세지가 남겨있고 + 이메일도 보내는 형태인 것

개발할 때 참고하자!
