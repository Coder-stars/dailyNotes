# encoding: utf-8
from tests import factories, utils


class TestAdserver(utils.RestTestCase):
    def setUp(self):
        self.user = factories.UserFactory()
        self.client.force_authenticate(user=self.user)
        self.baseurl = "/api/v1/adserver"
        self.obj = factories.AdServerFactory()

    def testList(self):
        response = self.client.get(self.baseurl)
        self.assertEqual(len(response.json().get("records")), 1)
    
    def testCreate(self):
        data = {"userId": self.user.id, "name": "adserver-create"}
    
        response = self.client.post(self.baseurl, data=data)
        self.assertEqual(response.json().get("name"), "adserver-create")
    
    def testUpdate(self):
        url = f"{self.baseurl}/{self.obj.id}"
    
        data = {"userId": self.user.id, "name": "adserver-update"}
        # import ipdb; ipdb.set_trace(context=10)
        response = self.client.put(url, data=data)
        self.assertEqual(response.json().get("name"), "adserver-update")
    
    def testRetrireve(self):
        url = f"{self.baseurl}/{self.obj.id}"
    
        response = self.client.get(url)
        self.assertEqual(response.json().get("id"), self.obj.id)
    
    def testUid(self):
        url = f"{self.baseurl}/{self.obj.id}"
        data = {
            "uid": {"OTT": "test-OTT", "MBL": "test-MBL", "DSK": "test-DSK"},
            "uid_type": {
                "OTT": "test-OTT",
                "MBL": "test-MBL",
                "DSK": "test-DSK",
            },
        }
        # import ipdb; ipdb.set_trace(context=10)
        response = self.client.put(url, data=data, format="json")
        self.assertEqual(
            response.json().get("uid", ""),
            {"OTT": "test-OTT", "MBL": "test-MBL", "DSK": "test-DSK"},
        )
        self.assertEqual(
            response.json().get("uid_type", ""),
            {"OTT": "test-OTT", "MBL": "test-MBL", "DSK": "test-DSK"},
        )
        data = {
            "uid": {"OTT": "error-422", "MBL": "", "DSK": ""},
            "uid_type": {"OTT": "", "MBL": "", "DSK": ""},
        }
        response = self.client.put(url, data=data, format="json")
        self.assertEqual(response.status_code, 422)  # 同一平台类型uid和uid_type必须同时配置
        self.assertEqual(
            response.json()["fields"]["error"][0]["message"],
            "同一平台类型的uid和uid_type必须同时配置",
        )
        data = {
            "uid": {"OTT": "", "MBL": "", "DSK": ""},
            "uid_type": {"OTT": "", "MBL": "", "DSK": ""},
        }
        response = self.client.put(url, data=data, format="json")
        self.assertEqual(response.status_code, 200)  # 更新为空测试
        self.assertEqual(
            response.json().get("uid", ""), {"OTT": "", "MBL": "", "DSK": ""}
        )
        self.assertEqual(
            response.json().get("uid_type", ""),
            {"OTT": "", "MBL": "", "DSK": ""},
        )
    
    # def testBox(self):
    #     data = {"box": 1}
    #     response = self.client.get(self.baseurl, data)
    #     self.assertEqual(len(response.json()["records"]), 1)