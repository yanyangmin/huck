# huck
LOOK LOOK
# 设置API鉴权
auth = tweepy.OAuthHandler(consumer_key, consumer_secret)
auth.set_access_token(access_token, access_token_secret)

# 创建API对象
api = tweepy.API(auth)

# 定义要监控的博主用户名
target_username = "TARGET_BLOGGER_USERNAME"

# 设定监控时间间隔（秒）
monitoring_interval = 300  # 5分钟

while True:
    try:
        # 获取博主的最新推文
        tweets = api.user_timeline(screen_name=target_username, count=5, tweet_mode="extended")

        # 遍历最新的推文
        for tweet in tweets:
            tweet_text = tweet.full_text
            tweet_id = tweet.id
            # 在这里，你可以添加更多的逻辑来处理推文，例如，检查是否包含特定关键词，发送通知等。

            # 打印推文文本
            print(f"Tweet ID: {tweet_id}")
            print(f"Tweet Text: {tweet_text}")
            print("=" * 30)

        # 等待一段时间，然后继续监控
        time.sleep(monitoring_interval)

    except tweepy.TweepError as e:
        print(f"An error occurred: {e}")

    except KeyboardInterrupt:
        print("Monitoring stopped.")
        break
