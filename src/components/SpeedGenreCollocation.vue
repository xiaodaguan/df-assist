<template>

  <div>


    <!-- 第二行：内容 -->
    <el-row>
      <!-- 左：结果 -->
      <el-col :span="4">
        <el-affix>
          <el-row>
            <el-result v-show="getSum()>=140" :title="getSum()+'%'" sub-title="合计攻速" icon="success"></el-result>
            <el-result v-show="getSum()<140" :title="getSum()+'%'" sub-title="合计攻速" icon="error"></el-result>
          </el-row>

          <el-row>
            <p>快速选择：</p>
          </el-row>
          <el-row>
            <el-button @click="this.form = this.pre1">双尊 龙袍 红12 升级武器装扮</el-button>
            <br/>
            <el-button @click="this.form = this.pre2">稀有天空 红10 克隆武器装扮</el-button>
          </el-row>
        </el-affix>


      </el-col>

      <!-- 中：主体 -->
      <el-col :span="15">
        <el-form :model="form">
          <el-divider>防具</el-divider>
          <el-form-item label="肩膀">
            <el-radio-group v-model="form.shoulder">
              <el-radio-button v-for="item in preset.shoulder" :label="item.value">
                <span :style="{color: item.hasConditionSpeed===1?'orange':'black'}">{{ item.name }}</span>
                <font color="gray" size="1" v-show="item.desc != null">{{ item.desc }}</font>
                [{{ item.value * 100 }}%]
              </el-radio-button>
            </el-radio-group>
          </el-form-item>

          <el-timeline>
            <el-timeline-item>
              <el-form-item label="肩膀贴膜(巴卡尼版本)" size="small">
                <el-radio-group v-model="form.shoulderSticker">
                  <el-radio-button v-for="item in preset.shoulderSticker" :label="item.value">
                    <span :style="{color: item.hasConditionSpeed===1?'orange':'black'}">{{ item.name }}</span>
                    <font color="gray" size="1" v-show="item.desc != null">{{ item.desc }}</font>
                    [{{ item.value * 100 }}%]
                  </el-radio-button>
                </el-radio-group>
              </el-form-item>

            </el-timeline-item>
          </el-timeline>


          <el-form-item label="胸">
            <el-radio-group v-model="form.coat">
              <el-radio-button v-for="item in preset.coat" :label="item.value">
                <span :style="{color: item.hasConditionSpeed===1?'orange':'black'}">{{ item.name }}</span>
                <font color="gray" size="1" v-show="item.desc != null">{{ item.desc }}</font>
                [{{ item.value * 100 }}%]
              </el-radio-button>
            </el-radio-group>

          </el-form-item>
          <el-form-item label="腰">
            <el-radio-group v-model="form.belt">
              <el-radio-button v-for="item in preset.belt" :label="item.value">
                <span :style="{color: item.hasConditionSpeed===1?'orange':'black'}">{{ item.name }}</span>
                <font color="gray" size="1" v-show="item.desc != null">{{ item.desc }}</font>
                [{{ item.value * 100 }}%]
              </el-radio-button>
            </el-radio-group>

          </el-form-item>

          <el-form-item label="下装">
            <el-radio-group v-model="form.trousers">
              <el-radio-button v-for="item in preset.trousers" :label="item.value">
                <span :style="{color: item.hasConditionSpeed===1?'orange':'black'}">{{ item.name }}</span>
                <font color="gray" size="1" v-show="item.desc != null">{{ item.desc }}</font>
                [{{ item.value * 100 }}%]
              </el-radio-button>
            </el-radio-group>
          </el-form-item>

          <el-timeline>
            <el-timeline-item>
              <el-form-item label="下装贴膜(巴卡尼版本)" size="small">
                <el-radio-group v-model="form.trousersSticker">
                  <el-radio-button v-for="item in preset.trousersSticker" :label="item.value">
                    {{ item.name }}
                    <font color="gray" size="1" v-show="item.desc != null">{{ item.desc }}</font>
                    [{{ item.value * 100 }}%]
                  </el-radio-button>
                </el-radio-group>
              </el-form-item>

            </el-timeline-item>
          </el-timeline>


          <el-form-item label="鞋">
            <el-radio-group v-model="form.shoes">
              <el-radio-button label=0 disabled="true">攻速鞋</el-radio-button>
            </el-radio-group>
          </el-form-item>

          <el-divider>首饰</el-divider>
          <el-form-item label="手镯">

            <el-radio-group v-model="form.bracelet">
              <el-radio-button v-for="item in preset.bracelet" :label="item.value">
                <span :style="{color: item.hasConditionSpeed===1?'orange':'black'}">{{ item.name }}</span>
                <font color="gray" size="1" v-show="item.desc != null">{{ item.desc }}</font>
                [{{ item.value * 100 }}%]
              </el-radio-button>
            </el-radio-group>
          </el-form-item>

          <el-form-item label="项链">

            <el-radio-group v-model="form.necklace">
              <el-radio-button v-for="item in preset.necklace" :label="item.value">
                <span :style="{color: item.hasConditionSpeed===1?'orange':'black'}">{{ item.name }}</span>
                <font color="gray" size="1" v-show="item.desc != null">{{ item.desc }}</font>
                [{{ item.value * 100 }}%]
              </el-radio-button>
            </el-radio-group>
          </el-form-item>

          <el-form-item label="戒指">
            <el-radio-group v-model="form.ring">
              <el-radio-button v-for="item in preset.ring" :label="item.value">
                <span :style="{color: item.hasConditionSpeed===1?'orange':'black'}">{{ item.name }}</span>
                <font color="gray" size="1" v-show="item.desc != null">{{ item.desc }}</font>
                [{{ item.value * 100 }}%]
              </el-radio-button>
            </el-radio-group>

          </el-form-item>

          <el-divider>特殊</el-divider>
          <el-form-item label="左槽">

            <el-radio-group v-model="form.auxiliary">
              <el-radio-button v-for="item in preset.auxiliary" :label="item.value">
                <span :style="{color: item.hasConditionSpeed===1?'orange':'black'}">{{ item.name }}</span>
                <font color="gray" size="1" v-show="item.desc != null">{{ item.desc }}</font>
                [{{ item.value * 100 }}%]
              </el-radio-button>
            </el-radio-group>

          </el-form-item>

          <el-form-item label="魔法石">


            <el-radio-group v-model="form.magicStone">
              <el-radio-button v-for="item in preset.magicStone" :label="item.value">
                <span :style="{color: item.hasConditionSpeed===1?'orange':'black'}">{{ item.name }}</span>
                <font color="gray" size="1" v-show="item.desc != null">{{ item.desc }}</font>
                [{{ item.value * 100 }}%]
              </el-radio-button>
            </el-radio-group>

          </el-form-item>

          <el-form-item label="耳环">
            <el-radio-group v-model="form.earrings">
              <el-radio-button v-for="item in preset.earrings" :label="item.value">
                <span :style="{color: item.hasConditionSpeed===1?'orange':'black'}">{{ item.name }}</span>
                <font color="gray" size="1" v-show="item.desc != null">{{ item.desc }}</font>
                [{{ item.value * 100 }}%]
              </el-radio-button>
            </el-radio-group>
          </el-form-item>

          <el-divider>特色</el-divider>


          <el-form-item label="称号">
            <el-radio-group v-model="form.title">
              <el-radio-button v-for="item in preset.title" :label="item.value">
                {{ item.name }}
                <font color="gray" size="1" v-show="item.desc != null">{{ item.desc }}</font>
                [{{ item.value * 100 }}%]
              </el-radio-button>
            </el-radio-group>
          </el-form-item>
          <el-form-item label="宠物">
            <el-radio-group v-model="form.pet">
              <el-radio-button v-for="item in preset.pet" :label="item.value">
                {{ item.name }}
                <font color="gray" size="1" v-show="item.desc != null">{{ item.desc }}</font>
                [{{ item.value * 100 }}%]
              </el-radio-button>
            </el-radio-group>
          </el-form-item>
          <el-form-item label="蓝宠装">
            <el-radio-group v-model="form.petEquip">
              <el-radio-button v-for="item in preset.petEquip" :label="item.value">
                {{ item.name }}
                <font color="gray" size="1" v-show="item.desc != null">{{ item.desc }}</font>
                [{{ item.value * 100 }}%]
              </el-radio-button>
            </el-radio-group>

          </el-form-item>
          <el-form-item label="快捷栏装备">

            <el-radio-group v-model="form.crest">
              <el-radio-button v-for="item in preset.crest" :label="item.value">
                {{ item.name }}
                <font color="gray" size="1" v-show="item.desc != null">{{ item.desc }}</font>
                [{{ item.value * 100 }}%]
              </el-radio-button>
            </el-radio-group>

          </el-form-item>

          <el-form-item label="徽章">
            <el-radio-group v-model="form.badgeMode">
              <el-radio label="1" style="height: 120%" border="border">
                <el-tag type="primary">玲珑攻速<font size="1">[2%]</font></el-tag> &nbsp; x &nbsp;
                <el-input-number v-model="form.exquisiteBadgeNum" :min="0" :max="10"></el-input-number> &nbsp;
                <el-tag type="primary">灿烂攻速<font size="1">[1.5%]</font></el-tag> &nbsp; x &nbsp;
                <el-input-number v-model="form.brightBadgeNum" :min="0" :max="10"></el-input-number> &nbsp;
                <el-tag type="primary">华丽攻速<font size="1">[1.1%]</font></el-tag> &nbsp; x &nbsp;
                <el-input-number v-model="form.gorgeousBadgeNum" :min="0" :max="10"></el-input-number> &nbsp;
              </el-radio>
              <br/>
              <el-radio label="2" style="height: 120%" border="border">
                <el-tag type="primary">手动输入总和：</el-tag>
                <el-input v-model=" form.badgeTotalMan
              " style="width: 120px">
                  <template #append>%</template>
                </el-input>
              </el-radio>

            </el-radio-group>


          </el-form-item>
          <el-form-item label="守护珠">
            <el-radio-group v-model="form.guardianBead">
              <el-radio-button v-for="item in preset.guardianBead" :label="item.value">
                {{ item.name }}
                <font color="gray" size="1" v-show="item.desc != null">{{ item.desc }}</font>
                [{{ item.value * 100 }}%]
              </el-radio-button>
            </el-radio-group>


          </el-form-item>
          <el-form-item label="武器装扮">
            <el-radio-group v-model="form.weaponDressUp">
              <el-radio-button v-for="item in preset.weaponDressUp" :label="item.value">
                {{ item.name }}
                <font color="gray" size="1" v-show="item.desc != null">{{ item.desc }}</font>
                [{{ item.value * 100 }}%]
              </el-radio-button>
            </el-radio-group>

          </el-form-item>
          <el-form-item label="装扮">

            <el-radio-group v-model="form.dressUp">
              <el-radio-button v-for="item in preset.dressUp" :label="item.value">
                {{ item.name }}
                <font color="gray" size="1" v-show="item.desc != null">{{ item.desc }}</font>
                [{{ item.value * 100 }}%]
              </el-radio-button>
              <el-radio style="display: block" border="border">
                <el-tag type="primary">手动输入：</el-tag>
                <el-input v-model="form.dressUpMan" style="width: 120px; height: 95%">
                  <template #append>%</template>
                </el-input>
              </el-radio>
            </el-radio-group>

          </el-form-item>
          <el-form-item label="辟邪玉">
            <el-input v-model="form.jade" placeholder="手动输入" style="width: 120px">
              <template #append>%</template>
            </el-input>
          </el-form-item>

        </el-form>
      </el-col>

      <el-col :span="1">

      </el-col>
      <!-- 右 -->
      <el-col :span="4">
        <el-row>

          <el-descriptions column="1">
            <el-descriptions-item label="# 攻速鞋说明">
              <el-image src="https://gldq123.com/wp-content/uploads/2022/10/frc-bd5ec0a8031828262df8bd328ce68572.png" style="width: 100%"></el-image>
              <br/>
              - 包括：<br/>
              <el-tag type="success">防具✅</el-tag>
              <el-tag type="success">首饰✅</el-tag>
              <el-tag type="success">特殊装备✅</el-tag>
              <el-tag type="success">时装(武器装扮)✅</el-tag>
              <el-tag type="success">徽章✅</el-tag>
              <el-tag type="success">宠物(宠物装备)✅</el-tag>
              <el-tag type="success">守护珠✅</el-tag>
              <el-tag type="success">称号✅</el-tag>
              <el-tag type="success">快捷栏装备✅</el-tag>
              <el-tag type="success">辟邪玉✅</el-tag>
              <el-tag type="success">名称装饰卡✅</el-tag>
              <br/>
              - 不包括：<br/>
              <el-tag type="danger">武器❌</el-tag>
              <el-tag type="danger">婚戒❌</el-tag>
              <el-tag type="danger">角色自身加成❌</el-tag>
              <br/>
              - 列出了常见的凑攻速手段，对着抠就行<br/>
              - <span style="color:darkred">部分装备有触发条件，注意橙色字体！</span><br/>
              <span style="color: green; ">- 愿攻速鞋no显示bug！</span><br/>
              - <a href="https://bbs.colg.cn/thread-8613292-1-1.html" target="_blank">有啥意见建议，可以到C站留言给我 &#128540; ...</a>

            </el-descriptions-item>

          </el-descriptions>
        </el-row>

      </el-col>

    </el-row>

  </div>

</template>

<script>
export default {
  name: "SpeedGenreCollocation",
  methods: {
    getSum() {
      return Number(Number(
          Number(this.form.shoulder)
          + Number(this.form.shoulderSticker)
          + Number(this.form.coat)
          + Number(this.form.belt)
          + Number(this.form.trousers)
          + Number(this.form.trousersSticker)
          + Number(this.form.shoes)
          + Number(this.form.bracelet)
          + Number(this.form.necklace)
          + Number(this.form.ring)
          + Number(this.form.auxiliary)
          + Number(this.form.magicStone)
          + Number(this.form.earrings)
          + Number(this.form.title)
          + Number(this.form.pet)
          + Number(this.form.petEquip)
          + Number(this.form.crest)

          + (this.form.badgeMode === "1" ? (Number(this.form.exquisiteBadgeNum) * 0.02 + Number(this.form.brightBadgeNum) * 0.015 + Number(
              this.form.gorgeousBadgeNum) * 0.011) : Number(this.form.badgeTotalMan) / 100)

          + Number(this.form.guardianBead)
          + Number(this.form.weaponDressUp)
          + (Number(this.form.dressUp) > 0 ? Number(this.form.dressUp) : Number(this.form.dressUpMan) / 100)
          + Number(Number(this.form.jade) / 100)
      ) * 100).toFixed(1);
    }
  },
  data() {
    return {

      "preset": {
        "shoulder": [{"name": "绽放的自然生命", "value": 0.1, "hasConditionSpeed": 1, "desc": "冰抗50+"},
          {"name": "猎龙", "value": 0.08},
          {"name": "自由之翼", "hasConditionSpeed": 1, "value": 0.3, "desc": "领主/稀有进入灼伤"},
          {"name": "隐匿之光(血）｜冰玉之蚀(毒)｜电磁搜索者(电)｜沙漠星芒(灼)", "hasConditionSpeed": 1, "value": 0.05, "desc": "自身进入对应异常"},
          {"name": "其他", "value": 0}],
        "shoulderSticker": [{"name": "冰花", "value": 0.03}, {"name": "其他", "value": 0}],
        "coat": [{"name": "大地馈赠", "hasConditionSpeed": 1, "value": 0.1, "desc": "火抗50+"}, {"name": "暗影流光｜冷静的谋略家｜蓝灵8速", "value": 0.08},
          {"name": "双面星云皮大衣", "value": 0.05}, {"name": "其他", "value": 0}],
        "belt": [{"name": "星灭光离(满)", "hasConditionSpeed": 1, "value": 0.45, "desc": "99+火抗"},
          {"name": "星灭光离(8)", "hasConditionSpeed": 1, "value": 0.4, "desc": "88+火抗"},
          {"name": "星灭光离(7)", "hasConditionSpeed": 1, "value": 0.35, "desc": "77+火抗"},
          {"name": "星灭光离(6)|深潜30速", "hasConditionSpeed": 1, "value": 0.3, "desc": "66+火抗"},
          {"name": "深潜30速+8速", "value": 0.38}, {"name": "其他", "value": 0}],
        "trousers": [{"name": "机械装甲", "hasConditionSpeed": 1, "value": 0.2, "desc": "+10"},
          {"name": "机械装甲", "hasConditionSpeed": 1, "value": 0.22, "desc": "+11"},
          {"name": "机械装甲", "hasConditionSpeed": 1, "value": 0.24, "desc": "+12"},
          {"name": "梵塔", "hasConditionSpeed": 1, "value": 0.38, "desc": "攻击触发，10%*3(CD0.1，持续5)"}, {"name": "其他", "value": 0}],
        "trousersSticker": [{"name": "暴食", "value": 0.08, "desc": "周围存在异常状态敌人"}, {"name": "其他", "value": 0}],
        "shoes": 0,
        "bracelet": [{"name": "收获之手｜动力导航包", "value": 0.08}, {"name": "恩特30速", "value": 0.3}, {"name": "恩特30速+8速", "value": 0.38},
          {"name": "其他", "value": 0}],
        "necklace": [{"name": "原子核", "hasConditionSpeed": 1, "value": 0.15, "desc": "250+属强"},
          {"name": "脉冲", "hasConditionSpeed": 1, "value": 0.5, "desc": "每攻击5次，5%*10(持续30)"},
          {"name": "黯星｜骑士", "hasConditionSpeed": 1, "value": 0.2, "desc": "半血｜前冲3秒"}, {"name": "其他", "value": 0}],
        "ring": [{"name": "双音1｜炽热的渴望之证", "hasConditionSpeed": 1, "value": 0.08, "desc": "吃1球"},
          {"name": "双音2", "hasConditionSpeed": 1, "value": 0.16, "desc": "吃2球"},
          {"name": "双音3", "hasConditionSpeed": 1, "value": 0.24, "desc": "吃3球"}, {"name": "其他", "value": 0}],
        "auxiliary": [{"name": "光学眼镜｜挖掘机1", "hasConditionSpeed": 1, "value": 0.05, "desc": "品级900｜1层，施放技能(持续10)"},
          {"name": "挖掘机3｜黎明圣杯", "hasConditionSpeed": 1, "value": 0.15, "desc": "3层，施放技能(持续10)｜手搓技能触发5%*3(持续10)"},
          {"name": "挖掘机5", "hasConditionSpeed": 1, "value": 0.25, "desc": "5层，施放技能(持续10)"}, {"name": "生命的喘息", "value": 0.08},
          {"name": "其他", "value": 0}],
        "magicStone": [{"name": "诅咒之心", "value": 0.08},
          {"name": "逆流之魂｜吞噬黑暗", "hasConditionSpeed": 1, "value": 0.15, "desc": "20+宠物｜攻击触发(CD30，持续30)"},
          {"name": "和平捍卫者", "hasConditionSpeed": 1, "value": 0.2, "desc": "自身出血"},
          {"name": "吞噬黑暗", "hasConditionSpeed": 1, "value": 0.3, "desc": "攻击触发(CD30，持续30)，被击触发(持续30)"}, {"name": "其他", "value": 0}],
        "earrings": [{"name": "战术信号弹", "hasConditionSpeed": 1, "value": 0.3, "desc": "攻击触发，2%*15(非攻击-2%/0.5s)"},
          {"name": "冰晶", "value": 0.08}, {"name": "其他", "value": 0}],
        "title": [{"name": "至尊", "value": 0.04}, {"name": "普通", "value": 0.03}],
        "pet": [{"name": "春节｜夏日(升级)", "value": 0.05}, {"name": "夏日(未升级)", "value": 0.03}, {"name": "其他", "value": 0.04},
          {"name": "无", "value": 0}],
        "petEquip": [{"name": "4速", "value": 0.04}, {"name": "1速", "value": 0.01}, {"name": "无", "value": 0}],
        "crest": [{"name": "神圣符咒(飓风)", "value": 0.08, "desc": "出血纹章"}, {"name": "蓝蓝海豚｜粉粉海豚", "value": 0.05, "desc": "21夏日"},
          {"name": "其他", "value": 0}],
        "exquisiteBadgeNum": 0,
        "badgeMode": "1",
        "brightBadgeNum": 0,
        "gorgeousBadgeNum": 4,
        "badgeTotalMan": 4.4,
        "guardianBead": [{"name": "神器", "value": 0.03}, {"name": "稀有", "value": 0.024}, {"name": "其他", "value": 0}],
        "weaponDressUp": [{"name": "克隆", "value": 0.04, "desc": "三速"}, {"name": "稀有克隆", "value": 0, "desc": "四维+技能lv"}],
        "dressUp": [{"name": "龙袍8", "value": 0.2}, {"name": "龙袍3+稀有天空5", "value": 0.19, "desc": "脸+胸+任一"},
          {"name": "稀有天空8", "value": 0.16}, {"name": "节日套", "value": 0.13}],
        "dressUpMan": 16,
        "jade": 0
      },
      "form": {
        "shoulder": 0,
        "shoulderSticker": 0,
        "coat": 0.08,
        "belt": 0.45,
        "trousers": 0.2,
        "trousersSticker": 0,
        "shoes": 0,
        "bracelet": 0,
        "necklace": 0.15,
        "ring": 0,
        "auxiliary": 0.05,
        "magicStone": 0.08,
        "earrings": 0,
        "title": 0.03,
        "pet": 0.05,
        "petEquip": 0.04,
        "crest": 0,
        "exquisiteBadgeNum": 0,
        "badgeMode": "1",
        "brightBadgeNum": 0,
        "gorgeousBadgeNum": 4,
        "badgeTotalMan": 4.4,
        "guardianBead": 0.03,
        "weaponDressUp": 0.04,
        "dressUp": 0.16,
        "dressUpMan": 16,
        "jade": 0,
      },
      "pre1": {
        "shoulder": 0,
        "shoulderSticker": 0,
        "coat": 0.08,
        "belt": 0.45,
        "trousers": 0.24,
        "trousersSticker": 0,
        "shoes": 0,
        "bracelet": 0,
        "necklace": 0.15,
        "ring": 0,
        "auxiliary": 0.05,
        "magicStone": 0.08,
        "earrings": 0,
        "title": 0.04,
        "pet": 0.05,
        "petEquip": 0.04,
        "crest": 0,
        "exquisiteBadgeNum": 4,
        "badgeMode": "1",
        "brightBadgeNum": 0,
        "gorgeousBadgeNum": 0,
        "badgeTotalMan": 4.4,
        "guardianBead": 0.03,
        "weaponDressUp": 0,
        "dressUp": 0.2,
        "dressUpMan": 16,
        "jade": 0,
      },
      "pre2": {
        "shoulder": 0,
        "shoulderSticker": 0,
        "coat": 0.08,
        "belt": 0.45,
        "trousers": 0.2,
        "trousersSticker": 0,
        "shoes": 0,
        "bracelet": 0,
        "necklace": 0.15,
        "ring": 0,
        "auxiliary": 0.05,
        "magicStone": 0.08,
        "earrings": 0,
        "title": 0.03,
        "pet": 0.05,
        "petEquip": 0.04,
        "crest": 0,
        "exquisiteBadgeNum": 0,
        "badgeMode": "1",
        "brightBadgeNum": 0,
        "gorgeousBadgeNum": 4,
        "badgeTotalMan": 4.4,
        "guardianBead": 0.03,
        "weaponDressUp": 0.04,
        "dressUp": 0.16,
        "dressUpMan": 16,
        "jade": 0,
      }

    }
  },

}
</script>

<style scoped>

</style>
