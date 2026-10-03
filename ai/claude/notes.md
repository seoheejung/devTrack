# Claude

<!-- devtrack-draft-id: 4a645768-45f3-4228-a6f2-4d2f0eba188f -->
<details>
<summary><strong>클로드코드에 &quot;대기열&quot; 기능이 없다는게.... 너무너무 불편하지 않으신가요?</strong></summary>

코덱스에는 현 작업이 완전히 끝나고 나서 전송되는 "대기열" 기능이 있는데 클로드코드는 없더라구요  

클로드한테 작업 하나 시켜놓으면.. 기다리는 동안 다음에 시킬 일이 계속 떠오르잖아요?  

```
--> "아.. 이거 끝나면 이 기능도 추가해야겠다."
--> "그다음엔 README도 정리해야 하는데."
```

코덱스에서는 다음 요청을 대기열에 넣어둘 수 있는데.. 클코에서는 그냥 메시지를 보내면 하던 작업이 끝나기도 전에 새 요청이 중간에 들어가더라구요..  

저는 지금 클로드가 잘하고 있으니, 그대로 건드리지 않고 그거 마저 다하고 다음에 했으면 하거든요.  

미리 보내자니 중간에 끼어들고, 안 보내자니 다음 요청 하나 보내려고 끝날 때까지 기다려야 하잖아요!  

**그래서 만든 게 /next입니다.**  

클로드가 일하는 중에..  

```
/next [다음에 할 일]
```

이렇게 보내두면  현재 작업이 완전히 끝난 후에 주입됩니다!  

여기서 설치 바로 하실 수 있습니다!  
https://github.com/Seokwoooo/claude-next  

설치는 터미널에서  

```
npx claude-next-skill
```

위의 명령어 한번 입력하시거나 AI한테 설치시키시려면 아래의 프롬프트 복붙하셔도 됩니다!  

```

Install the /next skill for Claude Code by running `npx -y claude-next-skill`.
If npx isn't available, download
https://raw.githubusercontent.com/Seokwoooo/claude-next/main/skills/next/SKILL.md
and save it unchanged as ~/.claude/skills/next/SKILL.md.
When it's done, tell me to open a new Claude Code session.
```



</details>

---
