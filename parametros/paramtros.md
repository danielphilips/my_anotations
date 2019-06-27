###  Select to get the deprecated parameters in of a function in HTML5:

select a.nr_seq_parametro nr_parametro,
substr((select obter_desc_expressao(x.CD_EXP_PARAMETRO,null) ds
	from funcao_parametro x 
	where x.cd_funcao = a.cd_funcao_param 
	and x.nr_sequencia = a.nr_seq_parametro),1,255) desc_parametro
from FUNCTION_RELEASE_NOTE a
where a.cd_funcao = 923
and a.nr_seq_parametro is not null
and a.DT_INATIVACAO is null
order by a.nr_seq_parametro;

###  Select to get the deprecated parameters in of a function in HTML5
that are being used in the schemetics registrations:

select * 
from REGRA_CONDICAO_ITEM
where cd_funcao = 923
and nr_seq_param in (select a.nr_seq_parametro
                  from FUNCTION_RELEASE_NOTE a
                  where a.cd_funcao = 923
                  and a.nr_seq_parametro is not null
                  and a.DT_INATIVACAO is null)
