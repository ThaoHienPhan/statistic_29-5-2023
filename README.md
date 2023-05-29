# statistic_29-5-2023

import React from 'react';
import PropTypes from 'prop-types';
import { AiOutlineArrowUp } from "react-icons/ai";
import { AiOutlineArrowDown } from "react-icons/ai";

Amount.propTypes = {
  data: PropTypes.array.isRequired,
};

function Amount({ data }) {
  return (
    <div className='w-full flex justify-between'>
      {data.map((item) => (
        <div key={item.id} className="bg-[#F3F3F3]/[.7] w-[300px] h-[150px] flex justify-center items-center rounded py-[10px]">
          <div>
            <p className="text-lg text-[#005072]">{item.name}</p> 
            <div className="text-5xl font-semibold text-[#005072] ">{item.amount}</div>
            <div className="text-small text-[green] mt-[7px] opacity-60 relative">
              {item.percentage >= 0 
              ? <div>
                <div className='inline-block absolute top-[3px] left-[33px]'>
                <AiOutlineArrowUp />
              </div>
              <div>
              {item.percentage}%
              </div>
                </div>
              : <div className='text-[red]'>
              <div className='inline-block absolute top-[3px] left-[33px]'>
              <AiOutlineArrowDown />
            </div>
            <div>
            {item.percentage}%
            </div>
              </div>
            }
            </div>
          </div>
        </div>
      ))}
    </div>
  );
}

export default Amount;


import React, { useEffect, useState } from "react";
import PropTypes from "prop-types";
import MonthBarChart from "./Chart/MonthBarChart";
import WeekBarChart from "./Chart/WeekBarChart";
import Switch from "./GeneralSwitch";
import SwitchInChart from "./SwitchInChart";
import Amount from "./Amount";
import { AiOutlineArrowDown } from "react-icons/ai";
import Filter from "./Dropdown";

Statictis.propTypes = {};

function Statictis(props) {
  const [option, setOption] = useState("Monthly");
  const [checkedArray, setCheckedArray] = useState([]);
  
  const data = [
    {
    name: "New Prototype",
    amount: 10000,
    percentage: 20
    },
   {
    name: "Run Prototype",
    amount: 10000,
    percentage: 10
    },
    {
    name: "Visit",
    amount: 11000,
    percentage: -10
    },
    {
      name: "New Feedback",
      amount: 82000,
      percentage: -10
      },
  ]

  const handleOption = (option) => {
    setOption(option);
  };

  const handleFilterChange = (checkedArray) => {
    setCheckedArray(checkedArray);
  };

  return (
    <div className="my-5 mx-28 select-none">
      <h1 className="inline-block text-5xl text-center bg-gradient-to-r from-[#005072] to-[#AEBD38] bg-clip-text text-transparent ">Statistic</h1>
      <div className="flex justify-end">
        <Switch handleOption={handleOption}/>  
      </div>
      <div className="py-[20px]">
          <SwitchInChart option={option} /> 
      </div>
      <div className="flex justify-end relative z-50">
        <Filter handleFilterChange={handleFilterChange} />
      </div>
      <div className="relative"> 
        <h2 className="text-2xl text-left text-[#005072] mb-[10px]">Prototype statistic</h2>
        <div className="bg-[#F3F3F3]/[.4] w-full rounded">
          <div className="w-[800px] m-auto ">
            {option === 'Monthly' ? <MonthBarChart checkedArray={checkedArray} /> : <WeekBarChart checkedArray={checkedArray}/>}
          </div>
        </div>
      </div>
      <div className="">
        <h2 className="text-2xl text-left text-[#005072] my-[20px]">Interactions statistic</h2>
        <div className="flex justify-between mt-[10px] text-center w-full">     
          {/* if more than 4 components => flex : nowarp */}
          <Amount data={data} />
        </div>
      </div>
    </div>
  );
}

export default Statictis;
