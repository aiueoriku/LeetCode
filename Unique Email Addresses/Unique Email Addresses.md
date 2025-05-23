# Step1
何も見ずに実行
```python
class Solution:
    def numUniqueEmails(self, emails: List[str]) -> int:
        valid_emails = []
        for email in emails:
            local, domain = email.split("@")
            local = local.replace(".", "")
            local = local.split("+")[0]
            email = local+"@"+domain
            if email not in valid_emails:
                valid_emails.append(email)
        return len(valid_emails)
```
emailをlocalとdomainに分割し，ルールに従い，domainを実際に有効な形式に変換した．単純にリストにappendして数えたが，dictを使ったらより計算効率が上がるかもしれない．

# Step2
他の人の解答を参照する．
https://github.com/potrue/leetcode/pull/14/files#diff-6a8efe56493bdbfeb045b7aa123660406ebdd5dd4f0a011935562d4eefb9ab46

上記を見ると，概ね実装方針は同じだった．ただ，以下が参考になった．
- listの代わりにset()を使っていたこと．setは重複を排除する．
- ＠が含まれない場合も考慮して，partitionを使用していたこと．partitionは区切り文字も返す．
  
また，RFC規格という存在を知った．https://info.yamap.com/archives/3434

# Step3
他の人の解答を参考に解き直す
```python
class Solution:
    def numUniqueEmails(self, emails: List[str]) -> int:
        valid_emails = set()
        for email in emails:
            local, at, domain = email.partition("@")
            local = local.replace(".", "")
            local = local.split("+")[0]
            email = local + at + domain
            valid_emails.add(email)
        return len(valid_emails)
```
# Step4
いただいたアドバイスを元に修正
```python
class Solution:
    def numUniqueEmails(self, emails: List[str]) -> int:
        valid_emails = set()
        for email in emails:
            local, at, domain = email.partition("@")
            local = local.split("+")[0]
            local = local.replace(".", "")
            email = f"{local}@{domain}"
            valid_emails.add(email)
        return len(valid_emails)
```
