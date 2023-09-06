def remtab(text):
    lines = text.split("\n")
    stripped_lines = [line.lstrip() for line in lines]
    return "\n".join(stripped_lines)
class virtualziosCopilot:
    def __init__(self, token):
        self.token=token
    def compileCode(self, inpu, lang=False):
        import requests
        api_url = "https://api.github.com/search/code"
        search_query ='"'+inpu.replace('"', "'")+'"'
        if lang:
            search_query+=" language:"+lang
        headers = {
            "Authorization": f"token {self.token}",
            "Accept": "application/vnd.github.v3+json",
        }
        params = {
            "q": search_query,
        }
        response = requests.get(api_url, headers=headers, params=params)
        data = response.json()
        try:
            for item in data['items']:
                link = item["html_url"].replace("github.com", "raw.githubusercontent.com").replace("/blob", "")
                res = requests.get(link)
                content = res.text
                for line in content.split("\n"):
                    if remtab(line).startswith(remtab(inpu)):
                        full= inpu.replace(remtab(inpu), remtab(line), 1)
                        return [full.replace(inpu, "", 1), link]
            return ""
        except KeyError:
            return ""
