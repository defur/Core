```


#include "core.h"

void handle_unit(t_obj *unit)
{
    t_obj *enemy;
    t_pos gem;

    enemy = core_get_nearest_enemy(unit);

    if (enemy)
    {
        core_action_attack(unit, enemy);
        return;
    }

    gem = core_get_nearest_gem(unit);
    core_action_moveTowards(unit, gem);
}

void bot_tick()
{
    t_obj **units;
    int count;
    int i;

    units = core_get_objs_filter(ft_is_own_team_unit);
    count = core_get_objs_filter_count(ft_is_own_team_unit);

    i = 0;
    while (i < count)
    {
        handle_unit(units[i]);
        i++;
    }

    if (core_get_gems() >= 10)
        core_action_createUnit(UNIT_WARRIOR);
}




```
```
void handle_unit(t_obj *unit)
{
    t_obj *enemy;
    t_pos gem;

    enemy = core_get_nearest_enemy(unit);

    if (enemy)
    {
        core_action_attack(unit, enemy);
        return;
    }

    gem = core_get_nearest_gem(unit);
    core_action_moveTowards(unit, gem);
}

void bot_tick()
{
    t_obj **units;
    int count;
    int i;

    units = core_get_objs_filter(ft_is_own_team_unit);
    count = core_get_objs_filter_count(ft_is_own_team_unit);

    i = 0;
    while (i < count)
    {
        handle_unit(units[i]);
        i++;
    }

    if (core_get_gems() >= 5)
        core_action_createUnit(UNIT_WARRIOR);
}
```




