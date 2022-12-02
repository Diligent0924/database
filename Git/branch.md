# Branch를 생성하여 따로 관리하기

### branch를 사용하는 이유는?
1. main branch에서 하다가 에러가 발생했을 때 되돌리기가 어려움
2. 여러 사람들과 협업할 때 수많은 Conflict가 날 수 있음
3. 기능 단위로 할 경우에 따로 분리해서 모듈식으로 붙여넣는것이 효율성이 좋음
4. 여러 Branch로 하기 때문에 효율성이 매우 뛰어남
   
### branch 생성 / 이동 / 삭제하기
1. 생성  
   * git branch [브랜치이름]
   * git switch -c [브랜치이름] : 생성하고 이동
2. 이동
   1. git switch [브랜치이름]
3. 삭제
   1. git branch -D [브랜치이름] : 강제 삭제
   
### branch merge하기
1. branch에서 git commit 까지 하여 해당 branch의 Repository에 저장되어 있는 상태로 유지
2. git switch main/branch로 이동
3. git pull로 Remote Repository에 있는 것을 들고옴
4. git merge [bracnh이름]으로 합침
5. git push로 내가 만든 것을 합쳐서 보내붐