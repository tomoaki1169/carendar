# calender APP(react 使用)
## 制作背景
「みんなと共有カレンダー」
友達と遊ぶ予定、家族の空いている時間を知るには相手に聞くという一手間が必要である。
家族は聞けるとして、友達に頻繁に聞くのもしつこいと思われてしまうと考えた。
業務用のカレンダーは多く出ている。
プライベート向けにカレンダーアプリを開発する


## DB設計
### userテーブル

|Column|Type|Options|
|------|----|-------|
|name|string|null: false|
|password|string|null: false|
|email|string|null: false|

#### Association
- has_many :group_users
- has_many :groups, through: :group_users
- has_many :group_messages
- has_many :user_comments

### user_commentsテーブル

|Column|Type|Options|
|------|----|-------|
|user_id|integer|null: false, foreign_key: true|
|send_user_id|integer|null: false, foreign_key: true|
|comment|string|null: false|

#### Association
- belongs_to :user

### group_usersテーブル

|Column|Type|Options|
|------|----|-------|
|user_id|integer|null: false, foreign_key: true|
|group_id|integer|null: false, foreign_key: true|

#### Association
- belongs_to :group
- belongs_to :user

## groupテーブル

|Column|Type|Options|
|------|----|-------|
|name|string|null: false|

### Association
- has_many :group_users
- has_many :users, through: :group_users
- has_many :tasks

### group_messagesテーブル

|Column|Type|Options|
|------|----|-------|
|user_id|integer|null: false, foreign_key: true|
|group_id|integer|null: false, foreign_key: true|
|messages|string|null: false|

#### Association
- belongs_to :group
- belongs_to :user

## taskテーブル

|Column|Type|Options|
|------|----|-------|
|group_id|integer|null: false, foreign_key: true|
|user_id|integer|null: false, foreign_key: true|
|task|string|null: false|
|task_start|time||
|task_end|time||
|date|datetime|null: false|

### Association
- belongs_to :group
- belongs_to :user