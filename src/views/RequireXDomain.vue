<template>
  <div class="container">
    <i-form ref="requirement" :model="requirement" :label-width="120" :rules="ruleValidate">
      <form-item :label="$t('requirex_requirement_type_label')" prop="reqType">
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

      <form-item :label="$t('requirex_requirement_name_label')" prop="name">
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

      <form-item :label="$t('requirex_requirement_imperative_label')" prop="imperative">
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

      <form-item :label="$t('requirex_requirement_system_name_label')" prop="systemName">
        <i-input
          v-model="requirement.systemName"
          :placeholder="$t('requirex_requirement_system_name_label')"
        />
      </form-item>

      <form-item :label="$t('requirex_requirement_system_activity_label')" prop="systemActivity">
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

      <div class="sub-form" v-if="isSystemActivity">
        <form-item :label="$t('requirex_requirement_user_label')" v-if="userInt">
          <i-input v-model="requirement.user" :placeholder="$t('requirex_requirement_user_label')"/>
        </form-item>
        <form-item :label="$t('requirex_requirement_system_label')" v-if="extInt">
          <i-input
            v-model="requirement.system"
            :placeholder="$t('requirex_requirement_system_label')"
          />
        </form-item>

        <form-item :label="$t('requirex_requirement_from_label')" v-if="extInt">
          <i-select
            v-model="requirement.from"
            :placeholder="$t('requirex_select')"
            :remote-method="onSystemActivityChange"
          >
            <i-option
              :value="$t('requirex_requirement_from_value_1')"
            >{{ $t('requirex_requirement_from1')}}</i-option>
            <i-option
              :value="$t('requirex_requirement_system_from_value_2')"
            >{{ $t('requirex_requirement_from2')}}</i-option>
          </i-select>
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

        <form-item :label="$t('requirex_requirement_system_condition_domain_label')">
          <i-switch v-model="requirement.systemCondition" size="large">
            <span slot="open">{{$t('requirex_requirement_yes')}}</span>
            <span slot="close">{{$t('requirex_requirement_no')}}</span>
          </i-switch>
        </form-item>

        <form-item
          :label="$t('requirex_requirement_description')"
          prop="desc"
          v-if="requirement.systemCondition"
        >
          <i-input
            v-model="requirement.systemConditionDescription"
            type="textarea"
            :autosize="{minRows: 2,maxRows: 5}"
            :placeholder="$t('requirex_requirement_system_condition_descrive_label')"
          ></i-input>
        </form-item>
      </div>

      <form-item>
        <i-button type="primary" @click="handleSubmit('requirement')">Submit</i-button>
        <i-button style="margin-left: 8px" @click="handleReset('requirement')">Cancel</i-button>
      </form-item>
    </i-form>

    <!-- Modal del mensaje-->
    <modal v-model="dialog" title="RequireX" @on-ok="ok" ok-text="ok">
      <h1 slot="header">
        <span>{{$t("app_requirex")}} - {{$t('requirex_application')}}</span>
      </h1>
      <p>{{msg}}</p>
      <div slot="footer">
        <Button type="info" size="small" @click="ok">{{$t("modal_ok")}}</Button>
      </div>
    </modal>
  </div>
</template>
 
<script src="//unpkg.com/vue/dist/vue.js"></script>
<script src="//unpkg.com/iview/dist/iview.min.js"></script>
<script>
export default {
  data() {
    return {
      //Modelo que se usa para controlar el requerimiento
      msg: "",
      requirement: {
        reqType: "",
        name: "",
        condition: false,
        conditionDescription: "",
        imperative: "",
        systemName: "",
        systemActivity: "",
        user: "",
        processVerb: "",
        object: "",
        system: "",
        from: "",
        processVerb: "",
        systemCondition: false,
        systemConditionDescription: ""
      },
      //Realizar validaciones del formulario
      ruleValidate: {
        msg: [
          {
            required: true,
            message: "Please select the requirement type",
            trigger: "change"
          }
        ],
        name: [
          {
            required: true,
            message: "The name cannot be empty",
            trigger: "blur"
          }
        ],
        imperative: [
          {
            required: true,
            message: "Please select the imperative",
            trigger: "change"
          }
        ],
        systemName: [
          {
            required: true,
            message: "The system or subsystem name cannot be empty",
            trigger: "blur"
          }
        ],
        systemActivity: [
          {
            required: true,
            message: "Please select the system activity",
            trigger: "change"
          }
        ]
      },
      isSystemActivity: false,
      userInt: false,
      autoAct: false,
      extInt: false,
      dialog: false
    };
  },
  methods: {
    //Realizar filtro de opciones al cambiar de actividades
    onSystemActivityChange() {
      this.isSystemActivity = true;
      //Capturar tipo de actividades del sistema
      var systemActivity = this.requirement.systemActivity;

      //Aplicar condiciones
      if (systemActivity == "userInt") {
        this.userInt = true;
        this.autoAct = false;
        this.extInt = false;
      } else if (systemActivity == "autoAct") {
        this.userInt = false;
        this.autoAct = true;
        this.extInt = false;
      } else if (systemActivity == "extInt") {
        this.userInt = false;
        this.autoAct = false;
        this.extInt = true;
      }
    },
    handleSubmit(name) {
      //Validar el formulario
      this.$refs[name].validate(valid => {
        if (valid) {
          //Reiniciar requerimiento
          this.msg = "";
          //Si hay una condición
          if (this.requirement.condition == true) {
            this.msg += this.requirement.conditionDescription + " ";
          }

          this.msg +=
            "The " +
            this.requirement.systemName +
            " " +
            this.requirement.imperative;

          //Validate system activity
          if (this.requirement.systemActivity == "autoAct") {
            this.msg +=
              " " +
              this.requirement.processVerb +
              " " +
              this.requirement.object;
          } else if (this.requirement.systemActivity == "userInt") {
            this.msg +=
              " provide the " + this.requirement.user + " the capacity ";
            this.msg +=
              " " +
              this.requirement.processVerb +
              " " +
              this.requirement.object;
          } else if (this.requirement.systemActivity == "extInt") {
            this.msg +=
              " have the capacity of " +
              this.requirement.processVerb +
              " " +
              this.requirement.object +
              " " +
              this.requirement.from +
              " the " +
              this.requirement.system;
          }

          //Validat conditions
          if (this.requirement.systemCondition) {
            this.msg += ", " + this.requirement.systemConditionDescription;
          }
          //this.$Message.success(this.msg);
          this.dialog = true;
        } else {
          this.$Message.error("Fail!");
          this.dialog = false;
        }
      });
    },
    handleReset(name) {
      this.$refs[name].resetFields();
    },
    ok() {
      this.dialog = false;
      // this.$Message.info("Clicked ok");
    },
    cancel() {
      // this.$Message.info("Clicked cancel");
    }
  }
};
</script>
 
 <style>
.container {
  padding-right: 15px;
  padding-left: 15px;
}
</style>