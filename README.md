- print("hellow world!")👋 Hi, I’m @xiaomaomami
- 👀 I’m interested in .yaoxi yaoxi..
- 🌱 I’m currently learning ..play games.
- 💞️ I’m looking to collaborate on .ide clliberation..
- 📫 How to reach me ...443144062@qq.com
- 😄 Pronouns: ...
- ⚡ Fun fact: ...life is like a bag full of sweet,you never no what will happen

<!---
xiaomaomami/xiaomaomami is a ✨ special ✨ repository because its `README.md` (this file) appears on your GitHub profile.
You can click the Preview link to take a look at your changes.
--->
use passport to contral users' accessment
# 定义用户角色和权限
USERS = {
    "user1": {"role": "normal", "usage": {"download": 5}},
    "vip1": {"role": "vip", "usage": {"download": 10}},
}

def check_vip_role(username):
    """验证用户是否为VIP"""
    return USERS.get(username, {}).get("role") == "vip"

def access_feature(username, feature):
    """检查用户是否有权限访问特定功能"""
    if not check_vip_role(username):
        print(f"{username} 非VIP用户，无权访问 {feature}")
        return False
    print(f"{username} VIP用户，允许访问 {feature}")
    return True

def use_feature(username, feature, interval=5):
    """限制功能使用频率"""
    if feature not in USERS[username]["usage"]:
        print(f"{feature} 功能未开放")
        return
    
    if USERS[username]["usage"][feature] >= 10:  # 总次数限制
        print(f"{username} {feature} 使用已达上限")
        return
    
    current_time = time.time()
    if feature in USERS[username] and "last_usage" in USERS[username][feature]:
        last_time = USERS[username][feature]["last_usage"]
        if current_time - last_time < interval:
            print(f"{feature} 使用过于频繁，请稍后再试")
            return
    
    # 更新使用记录
    USERS[username][feature]["usage"] += 1
    USERS[username][feature]["last_usage"] = current_time
    print(f"{username} 成功使用 {feature}")

# 示例使用
if __name__ == "__main__":
    import time
    use_feature("user1", "download")  # 非VIP用户被拒绝
    use_feature("vip1", "download")   # VIP用户首次成功
    time.sleep(3)
    use_feature("vip1", "download")   # VIP用户频繁使用被限制
    time.sleep(3)
    use_feature("vip1", "download")   # VIP用户间隔后再次成功
