<template>
  <div class="container">
    <i-form :model="requirement" :label-width="120">
      <form-item :label="$t('requirex_requirement_type_label')">
        <i-select v-model="requirement.reqType" :placeholder="$t('requirex_select')">
          <i-option
            :value="$t('requirex_requirement_type_value_1')"
          >{{ $t('requirex_requirement_type1')}}</i-option>
          <i-option
            :value="$t('requirex_requirement_type_value_2')"
          >{{ $t('requirex_requirement_type2')}}</i-option>
          <i-option
            :value="$t('requirex_requirement_type_value_3')"
          >{{ $t('requirex_requirement_type3')}}</i-option>
        </i-select>
      </form-item>

      <form-item :label="$t('requirex_requirement_name_label')">
        <i-input v-model="requirement.name" :placeholder="$t('requirex_requirement_name_label')"/>
      </form-item>

      <form-item :label="$t('requirex_requirement_condition_label')">
        <i-switch v-model="requirement.condition" size="large">
          <span slot="open">{{$t('requirex_requirement_yes')}}</span>
          <span slot="close">{{$t('requirex_requirement_no')}}</span>
        </i-switch>
      </form-item>

      <form-item
        :label="$t('requirex_requirement_description')"
        prop="desc"
        v-if="requirement.condition"
      >
        <i-input
          v-model="requirement.conditionDescription"
          type="textarea"
          :autosize="{minRows: 2,maxRows: 5}"
          :placeholder="$t('requirex_requirement_condition_descrive_label')"
        ></i-input>
      </form-item>

      <form-item :label="$t('requirex_requirement_type_label')">
        <i-select v-model="requirement.imperative" :placeholder="$t('requirex_select')">
          <i-option
            :value="$t('requirex_requirement_imperative_value_1')"
          >{{ $t('requirex_requirement_imperative1')}}</i-option>
          <i-option
            :value="$t('requirex_requirement_imperative_value_2')"
          >{{ $t('requirex_requirement_imperative2')}}</i-option>
          <i-option
            :value="$t('requirex_requirement_imperative_value_3')"
          >{{ $t('requirex_requirement_imperative3')}}</i-option>
        </i-select>
      </form-item>

      <form-item :label="$t('requirex_requirement_type_label')">
        <i-select
          v-model="requirement.systemActivity"
          :placeholder="$t('requirex_select')"
          :remote-method="onSystemActivityChange"
        >
          <i-option
            :value="$t('requirex_requirement_system_activity_value_1')"
          >{{ $t('requirex_requirement_system_activity1')}}</i-option>
          <i-option
            :value="$t('requirex_requirement_system_activity_value_2')"
          >{{ $t('requirex_requirement_system_activity2')}}</i-option>
          <i-option
            :value="$t('requirex_requirement_system_activity_value_3')"
          >{{ $t('requirex_requirement_system_activity3')}}</i-option>
        </i-select>
      </form-item>

      <div class="sub-form">
        <form-item :label="$t('requirex_requirement_user_label')">
          <i-input v-model="requirement.user" :placeholder="$t('requirex_requirement_user_label')"/>
        </form-item>

        <form-item :label="$t('requirex_requirement_process_verb_label')">
          <i-input
            v-model="requirement.processVerb"
            :placeholder="$t('requirex_requirement_process_verb_label')"
          />
        </form-item>

        <form-item :label="$t('requirex_requirement_object_label')">
          <i-input
            v-model="requirement.object"
            :placeholder="$t('requirex_requirement_object_label')"
          />
        </form-item>
      </div>

      <form-item>
        <Button type="primary">Submit</Button>
        <Button style="margin-left: 8px">Cancel</Button>
      </form-item>
    </i-form>
  </div>
</template>
 
<script src="//unpkg.com/vue/dist/vue.js"></script>
<script src="//unpkg.com/iview/dist/iview.min.js"></script>
<script>
export default {
  data() {
    return {
      requirement: {
        reqType: "",
        name: "",
        condition: false,
        conditionDescription: "",
        imperative: "",
        systemActivity: "",
        user: "",
        processVerb: "",
        object: ""
      }
    };
  },
  methods: {
    onSystemActivityChange() {
      alert(this.requirement.systemActivity);
    }
  }
};
</script>
 