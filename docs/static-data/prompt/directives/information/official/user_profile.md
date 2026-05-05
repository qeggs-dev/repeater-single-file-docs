## 用户设定

{% with -%}
  {%- set prefix = "用户名：\n" -%}
  {{- prefix -}}
  {%- if user_custom_name -%}
    **{{- user_custom_name -}}**
  {%- else -%}
    **{{- user_name -}}({{nick_name}})**
  {%- endif -%}
{%- endwith %}

{%- with -%}
  {%- set prefix = "\n用户年龄：" -%}
  {{- prefix -}}
  {%- if user_custom_age -%}
    **{{- user_custom_age -}}**
  {%- elif user_age -%}
    **{{- user_age -}}**
  {%- endif -%}
{%- endwith %}

{%- with -%}
  {%- set prefix = "\n用户性别：" -%}
  {%- if user_custom_gender -%}
    {{- prefix -}}
    **{{- user_custom_gender -}}**
  {%- elif user_gender -%}
    {{- prefix -}}
    **{{- user_gender -}}**
  {%- endif -%}
{%- endwith %}

{%- if user_profile -%}
用户设定：
{{user_profile}}
{%- endif %}