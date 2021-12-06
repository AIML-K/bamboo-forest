# Git Branching Guide

이 문서는 연구실 내 깃허브 사용 규칙을 정리한 문서입니다. 구체적인 코드 사용보단 추상적인 branching process를 다루고 있습니다.

Contents

1. Why Github?
2. What is important in git branching?
3. How to branch?


## Why Github?

> 깃허브는 분산 버전 관리 툴인 깃 저장소 호스팅을 지원하는 웹 서비스이다. 루비 온 레일스로 작성되었다. GitHub는 영리적인 서비스와 오픈소스를 위한 무상 서비스를 모두 제공한다. (Wiki)

Github는 협업을 통한 개발을 가능하게 해주는 툴입니다. 여러 사람이 같이 개발을 하다 보면 서로의 코드가 충돌하는 경우도 있고, 의도치 않게 나의 코드가 상대방의 코드를 변경/삭제하는 경우가 발생할 수 있습니다. 이를 방지하기 위해 각자가 자신의 독립된 작업 공간인 branch에서 작업할 필요가 있습니다. Github는 이러한 과정을 쉽고 직관적으로 만들어줍니다.

추상적인 작업 프로세스를 요약하면 다음과 같습니다.

1. 자신이 작업하게 될 repository(이하 repo)를 local machine(각자 일하고 있는 workstation)으로 받아온다. (git clone)
2. 해당 repo에서 자신이 작업하고자 하는 issue를 확인한다.
3. 해당 issue를 작업할 branch를 생성한다. (git branch, git checkout)
4. 작업을 진행하면서 수정사항을 기록(commit)한다. (git add, git commit)
5. 작업을 진행하면서 remote(github server) branch에 업데이트 한다. (git push, **절대로 master branch에 바로 push하지 말것**)
6. 작업이 어느정도 진행되면 변경 사항을 master(혹은 다른 node branch)에 반영하기 위해 pull request를 작성, reviwer을 지정한다.
7. review와 그에 따른 수정이 끝나면 merge를 진행한다.

조금 더 단순화하자면,

> 불러오기(clone) -> 개별 작업공간 생성(branch) -> 작업과 기록(commit) -> 부분 업데이트(push) -> 전체 업데이트(pull request/merge)

이렇게 정리할 수 있습니다.


## What is important in git branching?

이후 내용은 위의 process 중 '개별 작업공간 생성(branch)'부분, 그 중에서도 branch의 이름을 짓는 방법에 대한 내용입니다. 원활한 협업을 위해서 각 branch는 다음과 같은 정보를 담고 있어야 합니다.

- 누가 (Who)
- 언제 (When)
- 어디서 (Where)
- 무엇을 (What)
- 어떻게 (How)
- 왜 (Why)

이러한 정보들이 담겨 있어야 서로의 코드를 볼 때 '이건 뭘 바꾼 거냐, 언제 바꾼 거냐, 누가 바꿨냐'같은, 한두달 지나면 머릿속에서 휘발될 내용을 가지고 논쟁을 하지 않아도 됩니다.

다행히도 위의 내용 중 '언제'는 github commit 내역에, '어디서', '어떻게'는 수정된 코드 그 자체가 담고 있으므로 굳이 별도의 기록이 필요하지 않습니다. (다만 협업을 위해 개발단계의 코드에선 주석을 다는 습관을 들이도록 합시다.) '왜'의 경우는 그 수정에 해당하는 issue의 내용과 commit message(commit 시 작성할 수 있음)르 통해 어느 정도 해소할 수 있습니다. 

이제 남은 건 '누가'와 '무엇을'입니다. github commit 내역에 '누가'도 기억이 되긴 하지만 계정이 바뀐다든지, local machine과의 연결이 끊길 경우 수정자가 'Unknown'으로 바뀌는 문제가 있어서 다소 불안정합니다. '무엇을'의 경우 그럼 어떤 issue를 해결하기 위해 작성되었느냐에 대한 내용입니다. 이를 기록하는 다양한 방법이 있고, consensus의 문제입니다. 우리 연구실에선 두 가지를 branch 이름을 통해 해결하기로 합의했고, 다음 챕터에선 우리 연구실에서 사용하는 naming consensus에 대해 알아봅시다.


## How to branch?

> 원칙1: 각자 repository에서 합의한 바를 따른다.

일단 대원칙은 그렇습니다. 해당 repo의 관리자가 정한 규칙일 수도 있고, 구성원이 합의하여 정한 규칙일 수도 있습니다. 각 작업에 가장 적합한 방식이 있을 것이기에 이하 서술될 원칙2는 강제적인 것은 아닙니다. 다만 매번 합의를 진행할 수도 없고, 그럴 필요가 없는 경우가 많기에 별도의 합의가 없는 경우 아래의 규칙을 따릅니다.

> 원칙2: 별도의 합의가 없는 경우, "issue{n}_{writer}"의 형식을 따른다.

여기서 {n}은 자신이 해소하고자 하는 issue number, {writer}는 자신의 이름이나 닉네임을 의미합니다. (언어로 인한 시스템 충돌을 방지하기 위해 영어 닉네임 사용을 권장합니다.) 닉네임은 그 닉네임이 자신임을 알아볼 수 있어야 하며, 가급적이면 변동이 없는 편이 좋습니다. 

만약 자신이 어떤 내용을 실험해보고 싶은데 issue에 없는 경우, 스스로 issue를 작성하여 self-assign을 하면 됩니다.

자신의 branch가 expire(예컨대 merge가 완료됐거나 별도의 수정 없이 abort하기로 한 경우)된 경우 깨끗한 관리를 위해 local과 remote에 있는 해당 브랜치는 적절히 삭제하는 것을 권장합니다. 공용공간에서의 정리를 생활화하도록 합시다.

이를 통해 git branching에 필요한 내용을 간략히 살펴보았습니다. 이를 통해 우린 육하원칙을 branch에 담을 수 있습니다.


이후 수정/추가 사항이 있으면 부담 없이 수정 후 아래에 수정 주체와 일자를 기록 바랍니다.

작성 : @cth127 (20211202)