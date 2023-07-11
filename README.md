# ChatGPT Custom Plugin For API Gateway

This repo has source code for a **custom ChatGPT Plugin for API Gateway**. You can use it to add API Gateway features such as **authentication, security, traffic management, observability, caching,** and other functionalities for your backend APIs using ChatGPT UI and [Apache APISIX](https://apisix.apache.org/).

## How does it work?

As an example, in the [ChatGPT user interface](https://chat.openai.com/), if a user wants to introduce an API Gateway in front of an existing [Conference API](https://conferenceapi.azurewebsites.net/) to obtain details about a speaker's sessions and topics, the plugin is capable of receiving commands in the chat and then forwards the user's request to the Apache APISIX [Admin API](https://apisix.apache.org/docs/apisix/admin-api/), which create a [Route](https://apisix.apache.org/docs/apisix/terminology/route/) with the user-specified input configuration. This can be another approach to **using the Chatbot to configure the API Gateway features.** See sample output to the prompt below:

![Chatbot to configure the API Gateway features](https://static.apiseven.com/uploads/2023/07/11/5R8pO3sy_Untitled%20%289%29.png)

After the command runs successfully, APISIX creates the route and registers an [Upstream](https://apisix.apache.org/docs/apisix/terminology/upstream/) for our Conference backend API. So, you can access the API Gateway domain and URL path to get a response through the Gateway. For example, this GET request to [http://localhost:9080/speaker/1/sessions](http://localhost:9080/speaker/6/sessions) endpoint returns all speaker’s sessions from Conference API. You can also do basic operations like **get all routes and a route by Id** directly by asking ChatGPT.

## How to run it?

### Prerequisites

- Before you start, it is good to have a basic understanding of APISIX. Familiarity with API gateway, and its key concepts such as [routes](https://docs.api7.ai/apisix/key-concepts/routes), [upstream](https://docs.api7.ai/apisix/key-concepts/upstreams), [Admin API](https://apisix.apache.org/docs/apisix/admin-api/), [plugins](https://docs.api7.ai/apisix/key-concepts/plugins), and HTTP protocol will also be beneficial.
- [Docker](https://docs.docker.com/get-docker/) is used to install the containerized etcd and APISIX.
- Download [Visual Studio Code](https://code.visualstudio.com/) compatible with your operating system, or use any other code editor like [IntelliJ IDEA](https://www.jetbrains.com/idea/), [PyCharm](https://www.jetbrains.com/pycharm/), etc.
- To develop custom **ChatGPT Plugins** you need to have a [ChatGPT Plus](https://openai.com/blog/chatgpt-plus) account and [join the plugins waitlist](https://openai.com/waitlist/plugins).

To start the project run simply the following command from the project root directory:

```yaml
docker compose up
```

When you start the project, Docker downloads any images it needs to run. You can see that APISIX, etcd and Python app (`chatgpt-config`) services are running.

![ChatGPT Custom Plugin For API Gateway is running](https://static.apiseven.com/uploads/2023/07/09/fjdeTtHh_Untitled%20%2811%29.png)

### Connect the custom plugin to the ChatGPT interface

If you have a **Plus account**, we must first enable the plugin in GPT-4 since it is disabled by default. We need to go to the settings and click the beta option and click “Enable plugins”. Then click the plugins pop bar on the top of ChatGPT, navigate to “Plugin Store” and select “Develop your own plugin”. Provide the local host URL for the plugin (`localhost:5000`).

![Untitled](https://static.apiseven.com/uploads/2023/07/09/BXsrCUtY_ChatGPT%20screenshot%204.png)

After you click on “Find a manifest file”, if everything is set it up correctly, you will see ChatGPT validates both manifest and OpenAPI spec files successfully. 

![Untitled](https://static.apiseven.com/uploads/2023/07/09/TXjNTZ4h_ChatGPT%20screenshot%203.png)

### Step 3: Test the custom plugin

Now the plugin is connected to the ChatGPT interface, we can write a simple command:

![Ask ChatGPT to create a Route](https://static.apiseven.com/uploads/2023/07/09/BmW5Ce4m_Untitled%20%2810%29.png)

#### Other demo use cases:

1. Create a Route with a plugin.
![image](https://github.com/Boburmirzo/apisix-api-gateway-chatgpt-plugin/assets/14247607/3324aed6-d16c-48b4-8f5b-8a162e04d4fd)

2. Show all existing routes.
![image](https://github.com/Boburmirzo/apisix-api-gateway-chatgpt-plugin/assets/14247607/a4e390c4-1cb1-4055-a5cb-f765d861d9bf)


### Next steps

Now you can take the sample project as a foundation and improve functionalities by adding more APISIX [Admin API](https://docs.api7.ai/apisix/reference/admin-api) specifications to [openapi.yaml](https://github.com/Boburmirzo/apisix-api-gateway-chatgpt-plugin/blob/main/chatgpt-plugin-config/openapi.yaml) file to use plugins and add API consumers and more. Feel free to contribute to the GitHub project by raising pull requests.

### Community

🙋 [Join the Apache APISIX Community](https://apisix.apache.org/docs/general/join/)

🐦 [Follow us on Twitter](https://twitter.com/ApacheAPISIX)

📝 [Find us on Slack](https://join.slack.com/t/the-asf/shared_invite/zt-vlfbf7ch-HkbNHiU_uDlcH_RvaHv9gQ)

💁 [How to contribute page](https://apisix.apache.org/docs/general/how-to-contribute/)

### About the author

Follow me on Twitter: [@BoburUmurzokov](https://twitter.com/BoburUmurzokov)

Visit my blog: [www.iambobur.com](https://www.iambobur.com/)
