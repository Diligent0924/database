# Git을 되돌리고자 할 때 사용하는 방법

### 가장 최신 Commit을 확인하는 방법
git commit --amend 
git commit --amend -m '[Commit 이름]' : commit message 변경

### Commit에 있던 곳을 되돌리는 방법
1. reset
   1. git reset [--soft/--mixed/--hard/HEAD^]
   2. 그냥 git reset을 쓰면 --mixed이며 Working Directory로 보내준다.
   3. git reset --soft는 Staging Area로 보낸다.
   4. 기존 Commit 자체를 지워버리기 때문에 최소 가장 최근의 Commit은 날라가므로 매우 위험하다.
2. revert
   1. git revert [commit_id]로 되돌린다.
   2. 기존의 Commit은 그대로 둔채로 뒤로 되돌리기 때문에 Error나는 것을 최소화할 수 있다.