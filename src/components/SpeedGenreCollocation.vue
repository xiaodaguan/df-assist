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
          <el-divider>防具</el-divider>
          <el-form-item size="small" label="肩膀">
            <el-radio-group v-model="form.shoulder">
              <el-radio-button label=0.1>绽放的自然生命(冰)[10]</el-radio-button>
              <el-radio-button label=0.08>猎龙[8]</el-radio-button>
              <el-radio-button label=0.3>自由之翼(火)[30]</el-radio-button>
              <el-radio-button label=0>其他</el-radio-button>
            </el-radio-group>
          </el-form-item>
          <el-form-item size="small" label="胸">
            <el-radio-group v-model="form.coat">
              <el-radio-button label=0.1>大地馈赠(火)[10]</el-radio-button>
              <el-radio-button label=0.08>草人[8]</el-radio-button>
              <el-radio-button label=0>其他</el-radio-button>
            </el-radio-group>
          </el-form-item>
          <el-form-item size="small" label="腰">
            <el-radio-group v-model="form.belt">
              <el-radio-button label=0.45>星灭光离(99火抗)[45]</el-radio-button>
              <el-radio-button label=0.3>深潜[30]</el-radio-button>
              <el-radio-button label=0.38>深潜+8[38]</el-radio-button>
              <el-radio-button label=0>其他</el-radio-button>
            </el-radio-group>
          </el-form-item>

          <el-form-item size="small" label="下装">
            <el-radio-group v-model="form.trousers">
              <el-radio-button label=0.2>增幅裤子+10[20]</el-radio-button>
              <el-radio-button label=0.22>增幅裤子+11[22]</el-radio-button>
              <el-radio-button label=0.24>增幅裤子+12[24]</el-radio-button>
              <el-radio-button label=0.38>梵塔[38]</el-radio-button>
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
              <el-radio-button label=0.08>耐久手[8]</el-radio-button>
              <el-radio-button label=0.08>半血手[8]</el-radio-button>
              <el-radio-button label=0.3>恩特[30]</el-radio-button>
              <el-radio-button label=0.38>恩特+8[38]</el-radio-button>
              <el-radio-button label=0>其他</el-radio-button>
            </el-radio-group>
          </el-form-item>

          <el-form-item size="small" label="项链">
            <el-radio-group v-model="form.necklace">
              <el-radio-button label=0.15>原子核(250属强)[15]</el-radio-button>
              <el-radio-button label=0.5>近战项链[50]</el-radio-button>
              <el-radio-button label=0.2>低血项链(半血触发)[20]</el-radio-button>
              <el-radio-button label=0.2>前冲项链(前冲3秒)[20]</el-radio-button>
              <el-radio-button label=0>其他</el-radio-button>
            </el-radio-group>
          </el-form-item>

          <el-form-item size="small" label="戒指">
            <el-radio-group v-model="form.ring">
              <el-radio-button label=0.08>双音(1球)[8]</el-radio-button>
              <el-radio-button label=0.16>双音(2球)[16]</el-radio-button>
              <el-radio-button label=0.24>双音(3球)[24]</el-radio-button>
              <el-radio-button label=0>其他</el-radio-button>
            </el-radio-group>
          </el-form-item>

          <el-divider>特殊</el-divider>
          <el-form-item size="small" label="辅助">
            <el-radio-group v-model="form.auxiliary">
              <el-radio-button label=0.05>品级[5]</el-radio-button>
              <el-radio-button label=0.25>挖掘机[25]</el-radio-button>
              <el-radio-button label=0.08>低血[8]</el-radio-button>
              <el-radio-button label=0>其他</el-radio-button>
            </el-radio-group>
          </el-form-item>

          <el-form-item size="small" label="魔法石">
            <el-radio-group v-model="form.magicStone">
              <el-radio-button label=0.15>宠物[15]</el-radio-button>
              <el-radio-button label=0.08>破招[8]</el-radio-button>
              <el-radio-button label=0.15>吞噬黑暗[15]</el-radio-button>
              <el-radio-button label=0.3>吞噬黑暗(挨揍)[30]</el-radio-button>
              <el-radio-button label=0.0>其他</el-radio-button>
            </el-radio-group>
          </el-form-item>

          <el-form-item size="small" label="耳环">
            <el-radio-group v-model="form.earrings">
              <el-radio-button label=0.08>冰晶[8]</el-radio-button>
              <el-radio-button label=0>其他</el-radio-button>
            </el-radio-group>
          </el-form-item>

          <el-divider>特色</el-divider>
          <el-form-item size="small" label="称号">
            <el-radio-group v-model="form.title">
              <el-radio-button label=0.04>至尊[4]</el-radio-button>
              <el-radio-button label=0.03>普通[3]</el-radio-button>
            </el-radio-group>
          </el-form-item>
          <el-form-item size="small" label="宠物">
            <el-radio-group v-model="form.pet">
              <el-radio-button label=0.05>春季/夏日[5]</el-radio-button>
              <el-radio-button label=0.04>其他弱鸡[4]</el-radio-button>
              <el-radio-button label=0>无</el-radio-button>
            </el-radio-group>
          </el-form-item>
          <el-form-item size="small" label="4速蓝宠装">
            <el-radio-group v-model="form.petEquip">
              <el-radio-button label=0.04>有[4]</el-radio-button>
              <el-radio-button label=0>无</el-radio-button>
            </el-radio-group>
          </el-form-item>
          <el-form-item size="small" label="快捷栏装备">
            <el-radio-group v-model="form.crest">
              <el-radio-button label=0.08>出血纹章[8]</el-radio-button>
              <el-radio-button label=0.05>蓝蓝/粉粉海豚[5]</el-radio-button>
              <el-radio-button label=0>其他</el-radio-button>
            </el-radio-group>
          </el-form-item>
          <el-form-item size="small" label="徽章">
            <el-radio-group v-model="form.badge">
              <el-radio-button label=0.02>玲珑[2]</el-radio-button>
              <el-radio-button label=0.015>灿烂[1.5]</el-radio-button>
              <el-radio-button label=0.011>华丽[1.1]</el-radio-button>
            </el-radio-group>
            &nbsp; x &nbsp;<el-input-number v-model="form.badgeNum" label="数量" :min="0" :max="10"></el-input-number>
          </el-form-item>
          <el-form-item size="small" label="守护珠">
            <el-radio-group v-model="form.guardianBead">
              <el-radio-button label=0.03>神器[3]</el-radio-button>
              <el-radio-button label=0.024>稀有[2.4]</el-radio-button>
              <el-radio-button label=0>无</el-radio-button>
            </el-radio-group>
          </el-form-item>
          <el-form-item size="small" label="武器装扮">
            <el-radio-group v-model="form.weaponDressUp">
              <el-radio-button label=0.04>普通[4]</el-radio-button>
              <el-radio-button label=0>稀有/无[0]</el-radio-button>
            </el-radio-group>
          </el-form-item>
          <el-form-item size="small" label="装扮">
            <el-radio-group v-model="form.dressUp">
              <el-radio-button label=0.2>龙袍*8[20]</el-radio-button>
              <el-radio-button label=0.19>龙袍*3(脸胸)+天空*5[19]</el-radio-button>
              <el-radio-button label=0.16>天空*8[16]</el-radio-button>
              <el-radio-button label=0.12>节日套[12]</el-radio-button>
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
          + Number(this.form.badge) * Number(this.form.badgeNum)
          + Number(this.form.guardianBead)
          + Number(this.form.weaponDressUp)
          + Number(this.form.dressUp)
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
        "badge": 0.011,
        "badgeNum": 4,
        "guardianBead": 0.03,
        "weaponDressUp": 0.04,
        "dressUp": 0.16,
        "jade": 0,
      }
    }
  },

}
</script>

<style scoped>

</style>
