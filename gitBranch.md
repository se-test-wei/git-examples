# wei : git branch怎麼用
`git branch` 是 Git 用來**管理分支（branch）**的指令。你如果是在 VS Code 做作業，最常用的是下面這幾個。

### 1. 查看目前有哪些分支

```bash
git branch
```

例如：

```text
* main
  homework
  test
```

`*` 代表你現在所在的分支。

---

### 2. 建立新分支

```bash
git branch homework
```

這只會「建立」，**不會自動切過去**。

建立後：

```bash
git branch
```

會看到：

```text
* main
  homework
```

---

### 3. 建立並直接切換到新分支 ⭐

比較推薦直接用：

```bash
git switch -c homework
```

例如你現在在 `main`：

```bash
git switch -c homework
```

就會變成：

```text
  main
* homework
```

---

### 4. 切換分支

```bash
git switch main
```

或：

```bash
git switch homework
```

舊版 Git 也常看到：

```bash
git checkout main
```

---

### 5. 把分支推到 GitHub

假設你建立了：

```bash
git switch -c homework
```

先正常 commit：

```bash
git add .
git commit -m "完成作業"
```

第一次推上 GitHub：

```bash
git push -u origin homework
```

之後再推就只需要：

```bash
git push
```

---

### 6. 刪除分支

刪除本機分支：

```bash
git branch -d homework
```

如果 Git 不讓你刪除，確定要強制刪：

```bash
git branch -D homework
```

刪除 GitHub 上的分支：

```bash
git push origin --delete homework
```

---

### 7. 查看 GitHub 上的分支

```bash
git branch -r
```

例如：

```text
origin/main
origin/homework
origin/test
```

本機 + GitHub 全部：

```bash
git branch -a
```

會看到：

```text
* main
  homework
  remotes/origin/main
  remotes/origin/homework
```

---

### 如果你是要「把 GitHub 的整個分支抓到 VS Code」

這個跟你之前問的情況很像。

先：

```bash
git fetch origin
```

查看：

```bash
git branch -a
```

假設 GitHub 有：

```text
remotes/origin/homework
```

直接建立本機分支並切過去：

```bash
git switch -c homework --track origin/homework
```

之後：

```bash
git branch
```

應該會看到：

```text
  main
* homework
```

這樣你在 VS Code 裡就已經切到 GitHub 的 `homework` 分支了。

# wei : git checkout -b 和 branch 有何關係
有關係，而且很簡單：**`git checkout -b` = 建立分支 + 切換到那個分支**。

### 直接比較

| 指令                     | 功能                               |
| ---------------------- | -------------------------------- |
| `git branch test`      | 建立 `test` 分支，但**不切換**            |
| `git checkout -b test` | 建立 `test` 分支，並且**切換過去**          |
| `git switch -c test`   | 和 `checkout -b` 類似，也是**建立 + 切換** |
| `git checkout test`    | 切換到已存在的 `test` 分支                |

例如你現在：

```text
* main
```

執行：

```bash
git branch test
```

結果：

```text
* main
  test
```

你還是在 `main`。

如果執行：

```bash
git checkout -b test
```

結果：

```text
  main
* test
```

你已經切到 `test`。

### 所以可以記成

```text
git branch test
     ↓
建立分支

git checkout -b test
     ↓
建立分支
   +
切換分支
```

其中 `-b` 可以理解成 **branch（建立新分支）**。

現在比較新的 Git 通常推薦：

```bash
git switch -c test
```

但你在課堂、教學或老師的指令中看到：

```bash
git checkout -b test
```

**完全正常，兩者用途基本相同。**
