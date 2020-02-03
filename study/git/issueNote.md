# Issue notes for using Github

본문은 git을 사용하며 겪은 이슈들과 그 것들을 해결하는 과정들을 정리한 노트입니다.

<br />

### **_@리파지토리 복사(clone)하기_**

한번도 클론을 떠본적이 없다보니 첫단추 부터 꼬였었다.<br />
_import repo_ 로 받았더니 _pull이 되지 않았다.(매우당황)_<br />
git폴더 log기록엔 브랜치가 있는데 pull시키면 없다고 나오고 branch확인해도 없다고 나왔다. 주변에 물어보니 대체 뭘 한거냐고...<br />
알고보니 먼저 로컬에서 복제(클론)후 리파지토리 만들어서 올려주고 하는 방법을 사용한다는데 나는 이무슨 신박한 방법을 쓴건지<br />

```
git clone remote<클론할repo주소>
```

이렇게 하면 되는거였다!!

<br />

### **_@브랜치명 변경하기_**

- 참고링크 [[git린이 탈출기-branch 이름 변경하기](https://velog.io/@zansol/git%EB%A6%B0%EC%9D%B4-%ED%83%88%EC%B6%9C%EA%B8%B0-branch-%EC%9D%B4%EB%A6%84-%EB%B3%80%EA%B2%BD%ED%95%98%EA%B8%B0-g1jtzk99se)]

```
1. git branch -m <기존브랜치명> <바꿀브랜치명>
2. git push origin :<기존브랜치명>
3. git checkout <바꾼브랜치명>
4. git branch --unset-upstream //안내대로 쳤지만 바뀐게 없음
5. git push
6. git push --set-upstream origin <바꾼브랜치명>
7. github에 정상적으로 변경 적용됨 확인
```

1번을 실행하고 난후 `git branch -l` 로 보면 바뀐브랜치로 변경되어 나오지만 `git branch -a`로 확인해 보면 저장소에는 변경되지 않았다.<br/>
2번을 실행하면 기존브랜치가 삭제되었다는 결과가 보여지는데 `git branch -a`로 확해보면 여전히 변경되지 않았다.<br/>
3번 master에서 바꾼브랜치명으로 checkout 해주면 `Your branch is based on 'origin/<이전브랜치명>', but the upstream is gone. (use "git branch --unset-upstream" to fixup)`라고 나온다. 그래서 `git branch --unset-upstream`을 해줬지만 바뀐게 없었다.<br/>
5번을 실행하니 현재 브랜치<바꾼브랜치명>에 업스트림 사용 브랜치가 없다고 git push --set-upstream origin <바꾼브랜치명>하라고 안내가 나왔다.<br />
실행 후 `*[new branch] <바꾼브랜치명> -> <바꾼브랜치명>`이라는 결과가 떴고 github에도 정상적으로 변경된것을 확인 했다.

<br />

### **_@리파지토리 삭제하기_**

로컬은 그냥 폴더를 **통으로 삭제하면** 된다.<br />
원격저장소는 github에 해당 리파지토리 - setting - 스크롤 아래로 쭈우우욱 - Danger Zone 하단에 `Delete this repository`버튼 클릭 <br />
해당 repo에 관련된 모든것이 지워지고 되돌릴수 없다는 경고와 함께 그래도 삭제하려면 적으라는 문구를 안내해줌 - 글을 적고 password입력하면 성공적으로 삭제되었다는 안내가 뜸(완료)
