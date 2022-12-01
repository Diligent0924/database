# BufferPool이란 무엇인가?

### BufferPool의 정의
Data를 미리 저장해주는 곳으로서 HTML Cache와 비슷한 개념  
(Data를 미리 저장했다가 필요한 SQL이 날라오면 저장해둔 Data Page를 주는 방식)

### BufferPool의 전체확인 명령어
show status like '%innodb_buffer_pool%';  
=> 만약 Innodb_buffer_pool_dump_status가 not starting으로 되어있다면 buffer_pool 비활성화

### BufferPool을 사용하기 위한 명령어(default = off)
set global innodb_buffer_pool_dump_now=on;  
=> 대량의 데이터가 있을 경우에 효과 확인이 가능

### BufferPool load 상태 확인 ( 상태정보 : not start, Finished, loaded)
show status like 'innodb_buffer_pool_load_status';