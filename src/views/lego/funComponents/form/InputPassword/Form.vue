<!--
 * @Description: 
 * @Author: yamanashi12
 * @Date: 2019-05-10 10:18:19
 * @LastEditTime: 2020-06-22 11:05:29
 * @LastEditors: Please set LastEditors
 -->
<template>
  <el-form label-width="90px" :rules="rules" :model="item" ref="form">
    <ComponentFormHeadTabs>
      <template slot="base">
        <FoldWraper label="基础信息" :level="1">
          <el-form-item label="名称：" prop="label">
            <el-input v-model="item.label" />
          </el-form-item>
          <el-form-item label="提示文本：" prop="placeholder">
            <el-input v-model="item.placeholder" />
          </el-form-item>
          <el-form-item label="提示备注：" prop="remark">
            <el-input v-model="item.remark" />
          </el-form-item>
        </FoldWraper>
        <FoldWraper label="功能配置" :level="1">
          <el-form-item label="编辑禁用：" prop="">
            <el-switch
              v-model="item.editDisabled"
              active-text="开启"
              inactive-text="关闭" />
          </el-form-item>
          <el-form-item label="MD5加密" prop="">
            <el-switch
              v-model="item.md5"
              active-text="开启"
              inactive-text="关闭" />
          </el-form-item>
        </FoldWraper>
        <!-- 触发事件 -->
        <ValidatorDialog 
          :options="item.validator" 
          :rules="['required', 'maxLength', 'minLength', 'password', 'apiCheck', 'regex']"/>
        <slot />
      </template>
      <template slot="data">
        <FoldWraper label="数据配置" :level="2">
          <el-form-item label="字段名：" prop="key">
            <el-input v-model.trim="item.key" />
          </el-form-item>
        </FoldWraper>
      </template>
      <template slot="event">
        <CodePointEvent :data="item" :event="['componentCreated', 'componentWillDestroy']"></CodePointEvent>
      </template>
    </ComponentFormHeadTabs>
  </el-form>
</template>
<script>
import ValidatorDialog from '@/views/lego/edit/components/ValidatorDialog'
import baseData from './data'

export default {
  name: 'InputPasswordForm',
  components: { ValidatorDialog },
  data() {
    return {
      rules: baseData.rules
    }
  },
  props: {
    item: {
      type: Object,
      default() {
        return {}
      }
    }
  }
}
</script>
