<template>
  <div class="app-container">
    <!--工具栏-->
    <div class="head-container">
      <el-date-picker
        v-model="query.createTime"
        :default-time="['00:00:00','23:59:59']"
        type="daterange"
        range-separator=":"
        size="small"
        class="date-item"
        value-format="yyyy-MM-dd HH:mm:ss"
        start-placeholder="开始日期"
        end-placeholder="结束日期"
      />
      <rrOperation :crud="crud" />
      <!--如果想在工具栏加入更多按钮，可以使用插槽方式， slot = 'left' or 'right'-->
      <crudOperation :permission="permission" />
      <!--表单组件-->
      <el-dialog :close-on-click-modal="false" :before-close="crud.cancelCU" :visible.sync="crud.status.cu > 0" :title="crud.status.title" width="500px">
        <el-form ref="form" :model="form" :rules="rules" size="small" label-width="80px">
          <el-form-item label="id" prop="id">
            <el-input v-model="form.id" style="width: 370px;" />
          </el-form-item>
          <el-form-item label="保险公司ID">
            <el-input v-model="form.insuranceCompanyId" style="width: 370px;" />
          </el-form-item>
          <el-form-item label="商品类别ID">
            <el-input v-model="form.goodsCategoryId" style="width: 370px;" />
          </el-form-item>
          <el-form-item label="商品名称">
            <el-input v-model="form.goodsName" style="width: 370px;" />
          </el-form-item>
          <el-form-item label="产品代码">
            <el-input v-model="form.goodsNo" style="width: 370px;" />
          </el-form-item>
          <el-form-item label="销售价格">
            <el-input v-model="form.sellPrice" style="width: 370px;" />
          </el-form-item>
          <el-form-item label="市场价格">
            <el-input v-model="form.marketPrice" style="width: 370px;" />
          </el-form-item>
          <el-form-item label="成本价格">
            <el-input v-model="form.costPrice" style="width: 370px;" />
          </el-form-item>
          <el-form-item label="打折">
            <el-input v-model="form.discount" style="width: 370px;" />
          </el-form-item>
          <el-form-item label="上架时间">
            <el-input v-model="form.upTime" style="width: 370px;" />
          </el-form-item>
          <el-form-item label="下架时间">
            <el-input v-model="form.downTime" style="width: 370px;" />
          </el-form-item>
          <el-form-item label="浏览次数">
            <el-input v-model="form.visitCount" style="width: 370px;" />
          </el-form-item>
          <el-form-item label="收藏次数">
            <el-input v-model="form.favoriteCount" style="width: 370px;" />
          </el-form-item>
          <el-form-item label="评论次数">
            <el-input v-model="form.commentCount" style="width: 370px;" />
          </el-form-item>
          <el-form-item label="评分总数">
            <el-input v-model="form.grade" style="width: 370px;" />
          </el-form-item>
          <el-form-item label="销量">
            <el-input v-model="form.sale" style="width: 370px;" />
          </el-form-item>
          <el-form-item label="积分">
            <el-input v-model="form.score" style="width: 370px;" />
          </el-form-item>
          <el-form-item label="商品排序">
            <el-input v-model="form.sort" style="width: 370px;" />
          </el-form-item>
          <el-form-item label="img">
            <el-input v-model="form.img" style="width: 370px;" />
          </el-form-item>
          <el-form-item label="adImg">
            <el-input v-model="form.adImg" style="width: 370px;" />
          </el-form-item>
          <el-form-item label="商品状态:00正常 10已删除 20下架 30申请上架">
            <el-input v-model="form.goodsStatus" style="width: 370px;" />
          </el-form-item>
          <el-form-item label="栏目类别，用于区分页面显示比一比、看一看等栏目。">
            <el-input v-model="form.columnType" style="width: 370px;" />
          </el-form-item>
          <el-form-item label="库存">
            <el-input v-model="form.storeNums" style="width: 370px;" />
          </el-form-item>
          <el-form-item label="商品描述">
            <el-input v-model="form.goodsDescript" style="width: 370px;" />
          </el-form-item>
          <el-form-item label="关键字">
            <el-input v-model="form.keywords" style="width: 370px;" />
          </el-form-item>
          <el-form-item label="产品介绍">
            <el-input v-model="form.description" style="width: 370px;" />
          </el-form-item>
          <el-form-item label="searchWords">
            <el-input v-model="form.searchWords" style="width: 370px;" />
          </el-form-item>
          <el-form-item label="创建人">
            <el-input v-model="form.createAdmin" style="width: 370px;" />
          </el-form-item>
          <el-form-item label="创建时间">
            <el-input v-model="form.createTime" style="width: 370px;" />
          </el-form-item>
          <el-form-item label="更改时间">
            <el-input v-model="form.updateTime" style="width: 370px;" />
          </el-form-item>
          <el-form-item label="unit">
            <el-input v-model="form.unit" style="width: 370px;" />
          </el-form-item>
          <el-form-item label="brandId">
            <el-input v-model="form.brandId" style="width: 370px;" />
          </el-form-item>
          <el-form-item label="specArray">
            <el-input v-model="form.specArray" style="width: 370px;" />
          </el-form-item>
          <el-form-item label="exp">
            <el-input v-model="form.exp" style="width: 370px;" />
          </el-form-item>
          <el-form-item label="共享商品 0不共享 1共享">
            <el-input v-model="form.isShare" style="width: 370px;" />
          </el-form-item>
          <el-form-item label="0不推荐 1推荐">
            <el-input v-model="form.isRecommend" style="width: 370px;" />
          </el-form-item>
          <el-form-item label="label">
            <el-input v-model="form.label" style="width: 370px;" />
          </el-form-item>
          <el-form-item label="00-网信理财 10-销售销售">
            <el-input v-model="form.sellChannel" style="width: 370px;" />
          </el-form-item>
          <el-form-item label="00-租赁 10-销售">
            <el-input v-model="form.sellType" style="width: 370px;" />
          </el-form-item>
          <el-form-item label="businessId">
            <el-input v-model="form.businessId" style="width: 370px;" />
          </el-form-item>
          <el-form-item label=" 最后修改人">
            <el-input v-model="form.updateAdmin" style="width: 370px;" />
          </el-form-item>
          <el-form-item label="玩具类型">
            <el-input v-model="form.toyType" style="width: 370px;" />
          </el-form-item>
          <el-form-item label="锻炼能力">
            <el-input v-model="form.exerciseAbility" style="width: 370px;" />
          </el-form-item>
          <el-form-item label="适合年龄">
            <el-input v-model="form.fitAge" style="width: 370px;" />
          </el-form-item>
          <el-form-item label="玩具尺寸 大、中、小">
            <el-input v-model="form.size" style="width: 370px;" />
          </el-form-item>
          <el-form-item label="goldMemberPrice">
            <el-input v-model="form.goldMemberPrice" style="width: 370px;" />
          </el-form-item>
          <el-form-item label="memberPrice">
            <el-input v-model="form.memberPrice" style="width: 370px;" />
          </el-form-item>
          <el-form-item label="押金">
            <el-input v-model="form.deposit" style="width: 370px;" />
          </el-form-item>
          <el-form-item label="销售次数">
            <el-input v-model="form.shellNums" style="width: 370px;" />
          </el-form-item>
          <el-form-item label="分类ID">
            <el-input v-model="form.classifiedId" style="width: 370px;" />
          </el-form-item>
          <el-form-item label="重量">
            <el-input v-model="form.weight" style="width: 370px;" />
          </el-form-item>
          <el-form-item label="返佣比例">
            <el-input v-model="form.rebate" style="width: 370px;" />
          </el-form-item>
          <el-form-item label=" 10-实物  20-电子票">
            <el-input v-model="form.goodsType" style="width: 370px;" />
          </el-form-item>
        </el-form>
        <div slot="footer" class="dialog-footer">
          <el-button type="text" @click="crud.cancelCU">取消</el-button>
          <el-button :loading="crud.cu === 2" type="primary" @click="crud.submitCU">确认</el-button>
        </div>
      </el-dialog>
      <!--表格渲染-->
      <el-table ref="table" v-loading="crud.loading" :data="crud.data" size="small" style="width: 100%;" @selection-change="crud.selectionChangeHandler">
        <el-table-column type="selection" width="55" />
        <el-table-column v-if="columns.visible('id')" prop="id" label="id" />
        <el-table-column v-if="columns.visible('insuranceCompanyId')" prop="insuranceCompanyId" label="保险公司ID" />
        <el-table-column v-if="columns.visible('goodsCategoryId')" prop="goodsCategoryId" label="商品类别ID" />
        <el-table-column v-if="columns.visible('goodsName')" prop="goodsName" label="商品名称" />
        <el-table-column v-if="columns.visible('goodsNo')" prop="goodsNo" label="产品代码" />
        <el-table-column v-if="columns.visible('sellPrice')" prop="sellPrice" label="销售价格" />
        <el-table-column v-if="columns.visible('marketPrice')" prop="marketPrice" label="市场价格" />
        <el-table-column v-if="columns.visible('costPrice')" prop="costPrice" label="成本价格" />
        <el-table-column v-if="columns.visible('discount')" prop="discount" label="打折" />
        <el-table-column v-if="columns.visible('upTime')" prop="upTime" label="上架时间">
          <template slot-scope="scope">
            <span>{{ parseTime(scope.row.upTime) }}</span>
          </template>
        </el-table-column>
        <el-table-column v-if="columns.visible('downTime')" prop="downTime" label="下架时间">
          <template slot-scope="scope">
            <span>{{ parseTime(scope.row.downTime) }}</span>
          </template>
        </el-table-column>
        <el-table-column v-if="columns.visible('visitCount')" prop="visitCount" label="浏览次数" />
        <el-table-column v-if="columns.visible('favoriteCount')" prop="favoriteCount" label="收藏次数" />
        <el-table-column v-if="columns.visible('commentCount')" prop="commentCount" label="评论次数" />
        <el-table-column v-if="columns.visible('grade')" prop="grade" label="评分总数" />
        <el-table-column v-if="columns.visible('sale')" prop="sale" label="销量" />
        <el-table-column v-if="columns.visible('score')" prop="score" label="积分" />
        <el-table-column v-if="columns.visible('sort')" prop="sort" label="商品排序" />
        <el-table-column v-if="columns.visible('img')" prop="img" label="img" />
        <el-table-column v-if="columns.visible('adImg')" prop="adImg" label="adImg" />
        <el-table-column v-if="columns.visible('goodsStatus')" prop="goodsStatus" label="商品状态:00正常 10已删除 20下架 30申请上架" />
        <el-table-column v-if="columns.visible('columnType')" prop="columnType" label="栏目类别，用于区分页面显示比一比、看一看等栏目。" />
        <el-table-column v-if="columns.visible('storeNums')" prop="storeNums" label="库存" />
        <el-table-column v-if="columns.visible('goodsDescript')" prop="goodsDescript" label="商品描述" />
        <el-table-column v-if="columns.visible('keywords')" prop="keywords" label="关键字" />
        <el-table-column v-if="columns.visible('description')" prop="description" label="产品介绍" />
        <el-table-column v-if="columns.visible('searchWords')" prop="searchWords" label="searchWords" />
        <el-table-column v-if="columns.visible('createAdmin')" prop="createAdmin" label="创建人" />
        <el-table-column v-if="columns.visible('createTime')" prop="createTime" label="创建时间">
          <template slot-scope="scope">
            <span>{{ parseTime(scope.row.createTime) }}</span>
          </template>
        </el-table-column>
        <el-table-column v-if="columns.visible('updateTime')" prop="updateTime" label="更改时间">
          <template slot-scope="scope">
            <span>{{ parseTime(scope.row.updateTime) }}</span>
          </template>
        </el-table-column>
        <el-table-column v-if="columns.visible('unit')" prop="unit" label="unit" />
        <el-table-column v-if="columns.visible('brandId')" prop="brandId" label="brandId" />
        <el-table-column v-if="columns.visible('specArray')" prop="specArray" label="specArray" />
        <el-table-column v-if="columns.visible('exp')" prop="exp" label="exp" />
        <el-table-column v-if="columns.visible('isShare')" prop="isShare" label="共享商品 0不共享 1共享" />
        <el-table-column v-if="columns.visible('isRecommend')" prop="isRecommend" label="0不推荐 1推荐" />
        <el-table-column v-if="columns.visible('label')" prop="label" label="label" />
        <el-table-column v-if="columns.visible('sellChannel')" prop="sellChannel" label="00-网信理财 10-销售销售" />
        <el-table-column v-if="columns.visible('sellType')" prop="sellType" label="00-租赁 10-销售" />
        <el-table-column v-if="columns.visible('businessId')" prop="businessId" label="businessId" />
        <el-table-column v-if="columns.visible('updateAdmin')" prop="updateAdmin" label=" 最后修改人" />
        <el-table-column v-if="columns.visible('toyType')" prop="toyType" label="玩具类型" />
        <el-table-column v-if="columns.visible('exerciseAbility')" prop="exerciseAbility" label="锻炼能力" />
        <el-table-column v-if="columns.visible('fitAge')" prop="fitAge" label="适合年龄" />
        <el-table-column v-if="columns.visible('size')" prop="size" label="玩具尺寸 大、中、小" />
        <el-table-column v-if="columns.visible('goldMemberPrice')" prop="goldMemberPrice" label="goldMemberPrice" />
        <el-table-column v-if="columns.visible('memberPrice')" prop="memberPrice" label="memberPrice" />
        <el-table-column v-if="columns.visible('deposit')" prop="deposit" label="押金" />
        <el-table-column v-if="columns.visible('shellNums')" prop="shellNums" label="销售次数" />
        <el-table-column v-if="columns.visible('classifiedId')" prop="classifiedId" label="分类ID" />
        <el-table-column v-if="columns.visible('weight')" prop="weight" label="重量" />
        <el-table-column v-if="columns.visible('rebate')" prop="rebate" label="返佣比例" />
        <el-table-column v-if="columns.visible('goodsType')" prop="goodsType" label=" 10-实物  20-电子票" />
        <el-table-column v-permission="['admin','insGoodsInfo:edit','insGoodsInfo:del']" label="操作" width="150px" align="center">
          <template slot-scope="scope">
            <udOperation
              :data="scope.row"
              :permission="permission"
            />
          </template>
        </el-table-column>
      </el-table>
      <!--分页组件-->
      <pagination />
    </div>
  </div>
</template>

<script>
import crudInsGoodsInfo from '@/api/system/insGoodsInfo'
import CRUD, { presenter, header, form, crud } from '@crud/crud'
import rrOperation from '@crud/RR.operation'
import crudOperation from '@crud/CRUD.operation'
import udOperation from '@crud/UD.operation'
import pagination from '@crud/Pagination'

// crud交由presenter持有
const defaultCrud = CRUD({ title: '商品接口', url: 'api/insGoodsInfo', sort: 'id,desc', crudMethod: { ...crudInsGoodsInfo }})
const defaultForm = { id: null, insuranceCompanyId: null, goodsCategoryId: null, goodsName: null, goodsNo: null, sellPrice: null, marketPrice: null, costPrice: null, discount: null, upTime: null, downTime: null, visitCount: null, favoriteCount: null, commentCount: null, grade: null, sale: null, score: null, sort: null, img: null, adImg: null, goodsStatus: null, columnType: null, storeNums: null, goodsDescript: null, keywords: null, description: null, searchWords: null, createAdmin: null, createTime: null, updateTime: null, unit: null, brandId: null, specArray: null, exp: null, isShare: null, isRecommend: null, label: null, sellChannel: null, sellType: null, businessId: null, updateAdmin: null, toyType: null, exerciseAbility: null, fitAge: null, size: null, goldMemberPrice: null, memberPrice: null, deposit: null, shellNums: null, classifiedId: null, weight: null, rebate: null, goodsType: null }
export default {
  name: 'InsGoodsInfo',
  components: { pagination, crudOperation, rrOperation, udOperation },
  mixins: [presenter(defaultCrud), header(), form(defaultForm), crud()],
  data() {
    return {
      permission: {
        add: ['admin', 'insGoodsInfo:add'],
        edit: ['admin', 'insGoodsInfo:edit'],
        del: ['admin', 'insGoodsInfo:del']
      },
      rules: {
        id: [
          { required: true, message: '不能为空', trigger: 'blur' }
        ]
      }}
  },
  methods: {
    // 获取数据前设置好接口地址
    [CRUD.HOOK.beforeRefresh]() {
      return true
    }
  }
}
</script>

<style scoped>

</style>
