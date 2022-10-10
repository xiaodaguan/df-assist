<template>

  <div>

    <el-row>
      <el-col :span="4">
        <el-affix :offset="120">
          <el-result v-show="getSum()>=140" :title="getSum()+'%'" sub-title="合计攻速" icon="success"></el-result>
          <el-result v-show="getSum()<140" :title="getSum()+'%'" sub-title="合计攻速" icon="error"></el-result>
        </el-affix>
      </el-col>
      <el-col :span="20">
        <el-form :model="form">
          <el-descriptions title="">
            <el-descriptions-item>
              有啥意见建议，可以到C站留言给我 &#128540; ...<a href="https://bbs.colg.cn/thread-8613292-1-1.html" target="_blank">传送门</a>
            </el-descriptions-item>
          </el-descriptions>
          <el-divider>防具</el-divider>
          <el-form-item size="small" label="肩膀">
            <el-radio-group v-model="form.shoulder">
              <el-radio-button label=0.1>绽放的自然生命(冰)[10%]</el-radio-button>
              <el-radio-button label=0.08>猎龙[8%]</el-radio-button>
              <el-radio-button label=0.3>自由之翼(火)[30%]</el-radio-button>
              <el-radio-button label=0>其他</el-radio-button>
            </el-radio-group>
          </el-form-item>
          <el-form-item size="small" label="胸">
            <el-radio-group v-model="form.coat">
              <el-radio-button label=0.1>大地馈赠(火)[10%]</el-radio-button>
              <el-radio-button label=0.08>暗影流光|蓝灵自定义[8%]</el-radio-button>
              <el-radio-button label=0.05>双面星云皮大衣[5%]</el-radio-button>
              <el-radio-button label=0>其他</el-radio-button>
            </el-radio-group>
          </el-form-item>
          <el-form-item size="small" label="腰">
            <el-radio-group v-model="form.belt">
              <el-radio-button label=0.45>星灭光离(99火抗)[45%]</el-radio-button>
              <el-radio-button label=0.40>星灭光离(88火抗)[40%]</el-radio-button>
              <el-radio-button label=0.35>星灭光离(77火抗)[35%]</el-radio-button>
              <el-radio-button label=0.3>星灭光离(66火抗)|深潜自定义[30%]</el-radio-button>
              <el-radio-button label=0.38>深潜自定义+8[38%]</el-radio-button>
              <el-radio-button label=0>其他</el-radio-button>
            </el-radio-group>
          </el-form-item>

          <el-form-item size="small" label="下装">
            <el-radio-group v-model="form.trousers">
              <el-radio-button label=0.2>增幅裤子+10[20%]</el-radio-button>
              <el-radio-button label=0.22>增幅裤子+11[22%]</el-radio-button>
              <el-radio-button label=0.24>增幅裤子+12[24%]</el-radio-button>
              <el-radio-button label=0.38>梵塔基础裤子[38%]</el-radio-button>
              <el-radio-button label=0>其他</el-radio-button>
            </el-radio-group>
          </el-form-item>

          <el-form-item size="small" label="鞋">
            <el-radio-group v-model="form.shoes">
              <el-radio-button label=0>攻速鞋</el-radio-button>
            </el-radio-group>
          </el-form-item>

          <el-divider>首饰</el-divider>
          <el-form-item size="small" label="手镯">
            <el-radio-group v-model="form.bracelet">
              <el-radio-button label=0.08>收获之手|动力导航包[8%]</el-radio-button>
              <el-radio-button label=0.3>恩特自定义[30%]</el-radio-button>
              <el-radio-button label=0.38>恩特自定义+8[38%]</el-radio-button>
              <el-radio-button label=0>其他</el-radio-button>
            </el-radio-group>
          </el-form-item>

          <el-form-item size="small" label="项链">
            <el-radio-group v-model="form.necklace">
              <el-radio-button label=0.15>原子核(250属强)[15%]</el-radio-button>
              <el-radio-button label=0.5>脉冲触发器[50%]</el-radio-button>
              <el-radio-button label=0.2>黯星(半血触发)|骑士的赎罪(前冲3秒)[20%]</el-radio-button>
              <el-radio-button label=0>其他</el-radio-button>
            </el-radio-group>
          </el-form-item>

          <el-form-item size="small" label="戒指">
            <el-radio-group v-model="form.ring">
              <el-radio-button label=0.08>双音(1球)[8%]</el-radio-button>
              <el-radio-button label=0.16>双音(2球)[16%]</el-radio-button>
              <el-radio-button label=0.24>双音(3球)[24%]</el-radio-button>
              <el-radio-button label=0>其他</el-radio-button>
            </el-radio-group>
          </el-form-item>

          <el-divider>特殊</el-divider>
          <el-form-item size="small" label="辅助">
            <el-radio-group v-model="form.auxiliary">
              <el-radio-button label=0.05>光学眼镜｜挖掘机(1层)[5%]</el-radio-button>
              <el-radio-button label=0.15>挖掘机(3层)[15%]</el-radio-button>
              <el-radio-button label=0.25>挖掘机(满)[25%]</el-radio-button>
              <el-radio-button label=0.08>生命的喘息[8%]</el-radio-button>
              <el-radio-button label=0>其他</el-radio-button>
            </el-radio-group>
          </el-form-item>

          <el-form-item size="small" label="魔法石">
            <el-radio-group v-model="form.magicStone">
              <el-radio-button label=0.08>诅咒之心[8%]</el-radio-button>
              <el-radio-button label=0.15>逆流之魂(20宠物)|吞噬黑暗(不挨揍)[15%]</el-radio-button>
              <el-radio-button label=0.3>吞噬黑暗(挨揍)[30%]</el-radio-button>
              <el-radio-button label=0.0>其他</el-radio-button>
            </el-radio-group>
          </el-form-item>

          <el-form-item size="small" label="耳环">
            <el-radio-group v-model="form.earrings">
              <el-radio-button label=0.08>冰晶[8%]</el-radio-button>
              <el-radio-button label=0>其他</el-radio-button>
            </el-radio-group>
          </el-form-item>

          <el-divider>特色</el-divider>
          <el-form-item size="small" label="称号">
            <el-radio-group v-model="form.title">
              <el-radio-button label=0.04>至尊[4%]</el-radio-button>
              <el-radio-button label=0.03>普通[3%]</el-radio-button>
            </el-radio-group>
          </el-form-item>
          <el-form-item size="small" label="宠物">
            <el-radio-group v-model="form.pet">
              <el-radio-button label=0.05>春节|夏日[5%]</el-radio-button>
              <el-radio-button label=0.04>其他弱鸡[4%]</el-radio-button>
              <el-radio-button label=0>无</el-radio-button>
            </el-radio-group>
          </el-form-item>
          <el-form-item size="small" label="4速蓝宠装">
            <el-radio-group v-model="form.petEquip">
              <el-radio-button label=0.04>有[4%]</el-radio-button>
              <el-radio-button label=0>无</el-radio-button>
            </el-radio-group>
          </el-form-item>
          <el-form-item size="small" label="快捷栏装备">
            <el-radio-group v-model="form.crest">
              <el-radio-button label=0.08>出血纹章[8]</el-radio-button>
              <el-radio-button label=0.05>蓝蓝|粉粉海豚[5]</el-radio-button>
              <el-radio-button label=0>其他</el-radio-button>
            </el-radio-group>
          </el-form-item>
          <el-form-item size="small" label="徽章">
            <el-radio-group v-model="form.badgeMode">
              <el-radio label="1" style="display: block">组合：
                <el-tag type="primary">玲珑攻速[2%]</el-tag> &nbsp; x &nbsp;
                <el-input-number v-model="form.exquisiteBadgeNum" :min="0" :max="10"></el-input-number> &nbsp;
                <el-tag type="primary">灿烂攻速[1.5%]</el-tag> &nbsp; x &nbsp;
                <el-input-number v-model="form.brightBadgeNum" :min="0" :max="10"></el-input-number> &nbsp;
                <el-tag type="primary">华丽攻速[1.1%]</el-tag> &nbsp; x &nbsp;
                <el-input-number v-model="form.gorgeousBadgeNum" :min="0" :max="10"></el-input-number> &nbsp;
              </el-radio>
              <br/>
              <el-radio label="2" style="display: block">
                手动输入总和：
                <el-input v-model="form.badgeTotalMan" style="width: 120px" size="small">
                  <template #append>%</template>
                </el-input>
              </el-radio>

            </el-radio-group>


            <!--            <el-radio-group v-model="form.badge">-->
            <!--              <el-radio-button label=0.02>玲珑[2]</el-radio-button>-->
            <!--              <el-radio-button label=0.015>灿烂[1.5]</el-radio-button>-->
            <!--              <el-radio-button label=0.011>华丽[1.1]</el-radio-button>-->
            <!--            </el-radio-group>-->
            <!--            &nbsp; x &nbsp;<el-input-number v-model="form.badgeNum" label="数量" :min="0" :max="10"></el-input-number>-->
          </el-form-item>
          <el-form-item size="small" label="守护珠">
            <el-radio-group v-model="form.guardianBead">
              <el-radio-button label=0.03>神器[3%]</el-radio-button>
              <el-radio-button label=0.024>稀有[2.4%]</el-radio-button>
              <el-radio-button label=0>无</el-radio-button>
            </el-radio-group>
          </el-form-item>
          <el-form-item size="small" label="武器装扮">
            <el-radio-group v-model="form.weaponDressUp">
              <el-radio-button label=0.04>普通[4%]</el-radio-button>
              <el-radio-button label=0>稀有|无[0%]</el-radio-button>
            </el-radio-group>
          </el-form-item>
          <el-form-item size="small" label="装扮">
            <el-radio-group v-model="form.dressUp">
              <el-radio-button label=0.2>龙袍*8[20%]</el-radio-button>
              <el-radio-button label=0.19>龙袍*3(脸胸)+天空*5[19%]</el-radio-button>
              <el-radio-button label=0.16>天空*8[16%]</el-radio-button>
              <el-radio-button label=0.12>节日套[12%]</el-radio-button>
              <el-radio>
                手动输入
                <el-input v-model="form.dressUpMan" style="width: 120px" size="small">
                  <template #append>%</template>
                </el-input>
              </el-radio>
            </el-radio-group>
          </el-form-item>
          <el-form-item size="small" label="辟邪玉">
            <el-input v-model="form.jade" placeholder="手动输入" style="width: 120px">
              <template #append>%</template>
            </el-input>
          </el-form-item>

        </el-form>
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
          + Number(this.form.coat)
          + Number(this.form.belt)
          + Number(this.form.trousers)
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
      "form": {
        "shoulder": 0,
        "coat": 0.08,
        "belt": 0.45,
        "trousers": 0.2,
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
